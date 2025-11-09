using System;
using System.IO;
using System.Security.Cryptography;
using System.Text;

namespace IntegrityCheck
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.Write("Enter file path: ");
            string path = Console.ReadLine();

            if (!File.Exists(path))
            {
                Console.WriteLine("File not found!");
                return;
            }

            string hash = ComputeSHA256(path);
            Console.WriteLine($"SHA-256 Hash: {hash}");
        }

        static string ComputeSHA256(string filePath)
        {
            using (SHA256 sha = SHA256.Create())
            using (FileStream stream = File.OpenRead(filePath))
            {
                byte[] hash = sha.ComputeHash(stream);
                return BitConverter.ToString(hash).Replace("-", "");
            }
        }
    }
}
