#Abstract Factory

###Abstract Factory 
е създаващ шаблон за дизайн, който се използва в обектно-ориентираното програмиране.
Фабриката е средство за създаване на обекти. Целта на този шаблон за дизайн е да изолира създаването на обектите от тяхното използване.

Абстрактната фабрика капсулира група от методи Фабрика имащи близко предназначение. Клиентският код създава конкретна имплементация на абстрактната фабрика, след това използва основния интерфейс за да създава конкренти обекти. Клиентът не е задължен да знае коя от тези фабрики е създала конкретния обект, защото той използва само основния интерфейс към създадените обекти.

Този шаблон позволява замяната на конкретни класове, дори по време на изпълнение, без да е нужна промяна на кода, който ги използва. Това обаче е за сметка на на допълнително усложняване на кода, което не е много желателно.

using System;

  class MainApp
  {
    public static void Main()
    {
      AbstractFactory factory1 = new ConcreteFactory1();
      Client c1 = new Client(factory1);
      c1.Run();

      AbstractFactory factory2 = new ConcreteFactory2();
      Client c2 = new Client(factory2);
      c2.Run();

      Console.Read();
    }
  }

  // "AbstractFactory" 
  abstract class AbstractFactory
  {
    public abstract AbstractProductA CreateProductA();
    public abstract AbstractProductB CreateProductB();
  }

  // "ConcreteFactory1" 
  class ConcreteFactory1 : AbstractFactory
  {
    public override AbstractProductA CreateProductA()
    {
      return new ProductA1();
    }
    public override AbstractProductB CreateProductB()
    {
      return new ProductB1();
    }
  }

  // "ConcreteFactory2" 
  class ConcreteFactory2 : AbstractFactory
  {
    public override AbstractProductA CreateProductA()
    {
      return new ProductA2();
    }
    public override AbstractProductB CreateProductB()
    {
      return new ProductB2();
    }
  }

  // "AbstractProductA" 
  abstract class AbstractProductA
  {
  }

  // "AbstractProductB" 
  abstract class AbstractProductB
  {
    public abstract void Interact(AbstractProductA a);
  }

  // "ProductA1" 
  class ProductA1 : AbstractProductA
  {
  }

  // "ProductB1" 
  class ProductB1 : AbstractProductB
  {
    public override void Interact(AbstractProductA a)
    {
      Console.WriteLine(this.GetType().Name + " interacts with " + a.GetType().Name);
    }
  }

  // "ProductA2" 
  class ProductA2 : AbstractProductA
  {
  }

  // "ProductB2" 
  class ProductB2 : AbstractProductB
  {
    public override void Interact(AbstractProductA a)
    {
      Console.WriteLine(this.GetType().Name + " interacts with " + a.GetType().Name);
    }
  }

  // "Client" - the interaction environment of the products 
  class Client
  {
    private AbstractProductA AbstractProductA;
    private AbstractProductB AbstractProductB;

    // Constructor 
    public Client(AbstractFactory factory)
    {
      AbstractProductB = factory.CreateProductB();
      AbstractProductA = factory.CreateProductA();
    }

    public void Run()
    {
      AbstractProductB.Interact(AbstractProductA);
    }
  }
