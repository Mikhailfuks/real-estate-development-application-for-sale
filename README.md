using System;
using System.Collections.Generic;

namespace RealEstateApp
{
    // Класс для представления объекта недвижимости
    public class Property
    {
        public int Id { get; set; }
        public string Address { get; set; }
        public string Type { get; set; }
        public int Rooms { get; set; }
        public double Area { get; set; }
        public double Price { get; set; }
        public bool IsAvailable { get; set; }

        // Конструктор
        public Property(int id, string address, string type, int rooms, double area, double price, bool isAvailable)
        {
            Id = id;
            Address = address;
            Type = type;
            Rooms = rooms;
            Area = area;
            Price = price;
            IsAvailable = isAvailable;
        }
    }

    // Класс для управления списком недвижимости
    public class PropertyManager
    {
        private List<Property> properties = new List<Property>();

        // Добавление объекта недвижимости
        public void AddProperty(Property property)
        {
            properties.Add(property);
        }

        // Получение списка недвижимости
        public List<Property> GetProperties()
        {
            return properties;
        }

        // Поиск недвижимости по адресу
        public Property FindPropertyByAddress(string address)
        {
            return properties.Find(p => p.Address == address);
        }

        // Изменение статуса доступности недвижимости
        public void UpdateAvailability(int id, bool isAvailable)
        {
            Property property = properties.Find(p => p.Id == id);
            if (property != null)
            {
                property.IsAvailable = isAvailable;
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Создание менеджера недвижимости
            PropertyManager propertyManager = new PropertyManager();

            // Добавление объектов недвижимости
            propertyManager.AddProperty(new Property(1, "ул. Ленина 10", "Квартира", 2, 50, 1000000, true));
            propertyManager.AddProperty(new Property(2, "пр. Мира 15", "Дом", 4, 150, 5000000, true));
            propertyManager.AddProperty(new Property(3, "ул. Пушкина 20", "Квартира", 1, 30, 700000, true));

            // Вывод списка недвижимости
            Console.WriteLine("Доступная недвижимость:");
            foreach (Property property in propertyManager.GetProperties())
            {
                Console.WriteLine($"Id: {property.Id}, Адрес: {property.Address}, Тип: {property.Type}, Комнат: {property.Rooms}, Площадь: {property.Area} кв.м, Цена: {property.Price} руб.");
            }

            // Поиск недвижимости по адресу
            Property foundProperty = propertyManager.FindPropertyByAddress("ул. Ленина 10");
            if (foundProperty != null)
            {
                Console.WriteLine($"\nНайденная недвижимость: Id: {foundProperty.Id}, Адрес: {foundProperty.Address}");
            }
            else
            {
                Console.WriteLine("\nНедвижимость не найдена.");
            }

            // Изменение статуса доступности
            propertyManager.UpdateAvailability(1, false);
            Console.WriteLine("\nСтатус доступности обновлен.");

            Console.ReadKey();
        }
    }
}
