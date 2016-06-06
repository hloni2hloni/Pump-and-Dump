# Pump-and-Dump

using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading;

namespace PumpAndDump
{
    internal class Program
    {
        private static Thread dumpThread;
        private static Thread pumpThread;
        private static Random random = new Random();
        static List<int> values = new List<int>();
        public static IEnumerable<int> Pump()
        {
            while (true)
            {
                Thread.Sleep(random.Next(20, 100));
                yield return random.Next(0, 10);
            }
        }

        private static void Main()
        {
            StartPump();
            StartDump();
            Console.WriteLine("Running...");
            Console.WriteLine("Press any key to quit.");
            Console.ReadKey(true);
            dumpThread.Abort();
            pumpThread.Abort();
        }

        private static void StartDump()
        {
            dumpThread = new Thread(() =>
            {
                while (true)
                {
                    Thread.Sleep(TimeSpan.FromSeconds(20));
                    //todo: handle printing here
                }
            });

            dumpThread.Start();         
        }

        private static void StartPump()
        {
            pumpThread = new Thread(() =>
            {
                foreach (var value in Pump())
                {
                    //todo: handle getting data here
            });
            pumpThread.Start();
        }
    }
}
