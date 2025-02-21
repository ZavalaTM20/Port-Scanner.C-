using System;
using System.Net;
using System.Net.Sockets;
using System.Threading;

class PortScanner
{
    static void Main(string[] args)
    {
        Console.WriteLine("Welcome to the Basic Port Scanner!");

        // Get the target host and port range from the user
        Console.Write("Enter target IP or hostname (e.g., 192.168.1.1): ");
        string target = Console.ReadLine();
        Console.Write("Enter the start port number (e.g., 1): ");
        int startPort = int.Parse(Console.ReadLine());
        Console.Write("Enter the end port number (e.g., 1024): ");
        int endPort = int.Parse(Console.ReadLine());

        // Start scanning
        ScanPorts(target, startPort, endPort);
    }

    static void ScanPorts(string target, int startPort, int endPort)
    {
        // Scan ports using threads for faster results
        for (int port = startPort; port <= endPort; port++)
        {
            // Use a new thread for each port to speed up the scanning process
            ThreadPool.QueueUserWorkItem(ScanPort, new object[] { target, port });
        }

        // Keep the main thread alive to wait for all threads to finish
        Console.WriteLine("\nScanning in progress...");
        Console.ReadLine();
    }

    static void ScanPort(object obj)
    {
        var parameters = (object[])obj;
        string target = (string)parameters[0];
        int port = (int)parameters[1];

        try
        {
            // Create a TCP connection attempt
            using (TcpClient client = new TcpClient())
            {
                // Timeout set to 1000ms (1 second)
                client.ConnectAsync(target, port).Wait(1000);

                // If successful, the port is open
                Console.WriteLine($"Port {port} is OPEN on {target}");
            }
        }
        catch (Exception)
        {
            // If an error occurs (e.g., connection refused), the port is closed.
        }
    }
}
