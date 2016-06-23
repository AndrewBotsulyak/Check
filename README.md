using System;

class Program
{
    static void Main()
    {
        Check ch = new Check();  // struct
        Milk milk = new Milk();    // classes ... who inherit interface Product
        Beer beer = new Beer();
        Pepsi pepsi = new Pepsi();
        
        ch.AddProduct(milk, 3);
        ch.AddProduct(beer, 4);
        ch.AddProduct(pepsi, 1);

        ch.Print();

    }


    struct Check
    {
        private Product[] mas;     // Product - interface
        private int length;
        
        public void AddProduct(Product p, int count)
        {
            if (mas == null)
            {
                mas = new Product[length + 1];
                mas[length] = p;
                mas[length].Quantity = count;
                length++;
                return;
            }

            Product[] mas2 = mas;
            mas = new Product[length+1];
            Array.Copy(mas2, mas, length);
            mas[length] = p;
            mas[length].Quantity = count;
            length++;

        }

        public void ChangeName(string name, int pos)
        {
            if (pos < 0 || pos >= length)
                return;

            mas[pos].Name = name;
        }
        public void ChangeQuantity(int quantity, int pos)
        {
            if (pos < 0 || pos >= length)
                return;

            mas[pos].Quantity = quantity;
        }

        public void ChangePrice(double price, int pos)
        {
            if (pos < 0 || pos >= length)
                return;

            mas[pos].Price = price;
        }

        public void ChangeDiscount(int disc, int pos)
        {
            if (pos < 0 || pos >= length)
                return;

            mas[pos].Discount = disc;
        }

        public void Print()                              // Print()
        {
            Console.WriteLine("\t\t         Чек");
            Console.WriteLine("\t             Маг. Виртус");
            Console.WriteLine();
            Console.WriteLine(" Время покупки \t\t       {0}",DateTime.Now);
            Console.WriteLine();

            double discoun = 0;
            double all = 0;
            double sum;
            foreach(Product pr in mas)                 
            {
                sum = pr.Price - ((pr.Price * pr.Quantity)*pr.Discount) / 100;
                Console.WriteLine("{0,2}x {1,7} - price:   {2,4}  disc= {3,3}% | all: {4:f2}",
                    pr.Quantity, pr.Name, pr.Price, pr.Discount, sum);
                all += sum;
                discoun += ((pr.Price * pr.Quantity) * pr.Discount) / 100;
            }
            Console.WriteLine();
            Console.WriteLine(" Total sum\t\t\t\t   : {0:f2}",all);
            Console.WriteLine();
            Console.WriteLine("\t Общая сумма скидки составляет : {0:f2}",discoun);
            Console.WriteLine();
            Console.WriteLine(" Кассир : Наталья .\n\n Спасибо за покупку. \n\n Хорошего Дня!!");
            Console.WriteLine();
            Console.WriteLine("\t\t email : Virtus@mail.ru");
            Console.Read();

        }

        public ProductEnum GetEnumerator()
        {
            return new ProductEnum(mas);
        }

    }

    class ProductEnum
    {
        private Product[] arr;
        private int pos;
        public ProductEnum(Product[] mas)
        {
            arr = mas;
            pos = -1;
        }

        public bool MoveNext()
        {
            pos++;
            return pos < arr.Length;
        }

        public Product Current
        {
            get
            {
                return arr[pos];
            }
        }


    }

    interface Product 
    {
        string Name{get;set;}
        double Price{get;set;}
        int Quantity{ get; set; }
        int Discount { get; set; }
    }
    class Milk : Product
    {
        string name;
        double price;
        int quan;
        int disc;

        public Milk()
        {
            name = "Milk";
            price = 5.75;
            quan = 1;
            disc = 5;
        }
        public string Name
        {
            get { return name; }
            set { name = value; }
        }

        public double Price
        {
            get { return price; }
            set { price = value; }
        }

        public int Quantity
        {
            get { return quan; }
            set { quan = value; }
        }

        public int Discount
        { 
            get 
            {
                return disc;
            }
            set
            {
                disc = value;
            }
        }
    }

    class Beer : Product
    {
        string name;
        double price;
        int quan;
        int disc;

        public Beer()
        {
            name = "Beer";
            price = 7.40;
            quan = 1;
            disc = 7;
        }
        public string Name
        {
            get { return name; }
            set { name = value; }
        }

        public double Price
        {
            get { return price; }
            set { price = value; }
        }

        public int Quantity
        {
            get { return quan; }
            set { quan = value; }
        }
        public int Discount
        {
            get
            {
                return disc;
            }
            set
            {
                disc = value;
            }
        }
    }

    class Pepsi : Product
    {
        string name;
        double price;
        int quan;
        int disc;

        public Pepsi()
        {
            name = "Pepsi";
            price = 7.40;
            quan = 1;
            disc = 15;
        }
        public string Name
        {
            get { return name; }
            set { name = value; }
        }

        public double Price
        {
            get { return price; }
            set { price = value; }
        }

        public int Quantity
        {
            get { return quan; }
            set { quan = value; }
        }
        public int Discount
        {
            get
            {
                return disc;
            }
            set
            {
                disc = value;
            }
        }
    }

}
