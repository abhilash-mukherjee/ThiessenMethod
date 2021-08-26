# ThiessenMethod
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Learn_CS_24_Thiessen_MEthod
{
    public static class Helper
    {
        public static float Distance(Point a, Point b)
        {
            float distSquare = (float)((a.x - b.x)*(a.x - b.x) + (a.y - b.y)*(a.y - b.y));
            return (float)Math.Sqrt(distSquare);
        }
        public static void Input(int n, List<Point> points)
        {
            for(int i=0;i<n;i++)
            {
                float x, y, rainfall;
                Console.WriteLine($"P{i + 1}: ");
                Console.WriteLine($"X coodinate: ");
                x = float.Parse(Console.ReadLine());
                Console.WriteLine($"Y coodinate: ");
                y = float.Parse(Console.ReadLine());
                Point p = new Point(x, y);
                Console.WriteLine($"RainFall: ");
                rainfall = float.Parse(Console.ReadLine());
                p.rainfall = rainfall;
                points.Add(p);
            }
        }
    }
    public class Point
    {
        public float x;
        public float y;
        public float surroundingPointCount = 0;
        public float rainfall;
        public Point(float x, float y)
        {
            this.x = x;
            this.y = y;
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            float step = 0.1f;
            Console.WriteLine("Number Of Points: ");
            int n = Int32.Parse(Console.ReadLine());
            List<Point> points = new List<Point>();
            Helper.Input(n, points);
            
            float x = step/2;
            int count = 0;
            while (x < 5f)
            {
                float y = step/2;
                while ((y < 6f))
                {
                    Point point = new Point(x + step / 2, y + step / 2);
                    var distances = new List<float>();
                    for(int i =0;i<8;i++)
                    {
                        distances.Add(Helper.Distance(points[i], point));
                    }
                    points[distances.IndexOf(distances.Min())].surroundingPointCount++;
                    y += step;
                    count++;
                }

                x += step;
            }
            float area = 0f;
            for(int i=0;i<n;i++)
            {
                Console.WriteLine($"P{i+1}({points[i].x},{points[i].y}) -> a{i+1} = {points[i].surroundingPointCount * step * step}, r{i+1} = {points[i].rainfall}c.m");
                area += points[i].surroundingPointCount * step * step;
            }
            Console.WriteLine($"Total Area = { area}");
            float totalRainfall = 0;
            for(int i=0;i<n;i++)
            {
                totalRainfall += points[i].rainfall * points[i].surroundingPointCount * step * step;
            }
            Console.WriteLine($"Avg rainfall = (1/total area) * summation(ai * Ri) = 1/({area} * {totalRainfall} = {totalRainfall / area} c.m)");
            Console.ReadLine();
        }
    }
}

                                 Output:
                                 ![image](https://user-images.githubusercontent.com/84319482/130967470-9d6a4b60-b9fd-4328-b67a-a3fa28488209.png)
