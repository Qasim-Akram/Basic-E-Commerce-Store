Overview:

This code represents a simple e-commerce store system. It includes a catalog of products, allows users to add products to their cart, and provides a checkout functionality.

Classes:

.Product

.Electronics (extends Product)

.Clothes (extends Product)

.ECommerceStore

Class Details:

1. Product Class
   
This class represents a generic product with basic attributes: name, price, and category.


class Product {

    private String name;
    private int price;
    private String category;

    public Product(String name, int price, String category) {
        this.name = name;
        this.price = price;
        this.category = category;
    }

    public String getName() {
        return name;
    }

    public int getPrice() {
        return price;
    }

    public String getCategory() {
        return category;
    }

    @Override
    public String toString() {
        return "Product: " + name + ", Price: " + price + " PKR, Category: " + category;
    }}

Fields: 

name, price, category.

Constructor: 

Initializes these fields.

Getters: 

For each field.

toString() Method:

Provides a string representation of the product.

2. Electronics Class

This class represents electronics products. It extends the Product class and sets the category to "Electronics".


class Electronics extends Product {
    public Electronics(String name, int price) {
        super(name, price, "Electronics");
    }
}

3. Clothes Class

This class represents clothing products. It extends the Product class and sets the category to "Clothes".


class Clothes extends Product {
    public Clothes(String name, int price) {
        super(name, price, "Clothes");
    }
}

4. ECommerceStore Class

This class manages the store's products and shopping cart.







class ECommerceStore {

    private Product[] products;
    
    private int[] cart;
    
    private int cartSize;
    
    public ECommerceStore() {
       
        products = new Product[1];
        cart = new int[10];
        cartSize = 0;
        initializeStore();


        
    }
    private void initializeStore() {
        products[0] = new Electronics("Laptop", 99999);
        products[1] = new Electronics("Smartphone", 49999);
        products[2] = new Electronics("Headphones", 14999);
        products[3] = new Clothes("Shirt", 599);
        products[4] = new Clothes("Jeans", 1499);
        products[5] = new Clothes("Shoes", 2999);
        products[6] = new Clothes("Cape", 250);
    }

    public void displayAvailableItems() {
        System.out.println("Available Products:");
        for (int i = 0; i < products.length; i++) {
            if (products[i] != null) {
                System.out.println((i + 1) + ". " + products[i]);
            }
        }
    }

    public void addToCart(int productIndex) {
        if (cartSize < cart.length) {
            cart[cartSize++] = productIndex;
            System.out.println(products[productIndex].getName() + " added to the cart.");
        } else {
            System.out.println("Cart is full. Cannot add more products.");
        }
    }

    public void checkout() {
        int total = 0;
        System.out.println("Items in the cart:");
        for (int i = 0; i < cartSize; i++) {
            int productIndex = cart[i];
            System.out.println(products[productIndex]);
            total += products[productIndex].getPrice();
        }
        System.out.println("The total amount for checkout is: " + total + " PKR");
        
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter your amount");
        int amount = scanner.nextInt();
        
        if (amount == total) {
            System.out.println("Order Successful!!");
        } else {
            System.out.println("Entered amount should match the total order amount.");
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ECommerceStore store = new ECommerceStore();

        store.displayAvailableItems();

        while (true) {
            System.out.println("Enter the number of the product to add to the cart (0 to checkout):");
            int input = scanner.nextInt();
            if (input == 0) {
                store.checkout();
                break;
            } else if (input > 0 && input <= store.products.length) {
                store.addToCart(input - 1); // Adjusting for 0-based index
            } else {
                System.out.println("Invalid input. Please try again.");
            }
        }
        scanner.close();
    }
}
ECommerceStore Class Breakdown

Fields:

products: An array to store available products.

cart: An array to store indices of products added to the cart.

cartSize: Keeps track of the number of items in the cart.

Constructor:

Initializes products and cart arrays.

Calls initializeStore to add products to the store.

Methods:

initializeStore(): Adds predefined products to the products array.

displayAvailableItems(): Displays all available products in the store.

addToCart(int productIndex): Adds a product to the cart by its index if there is space.

checkout(): Displays items in the cart, calculates the total price, and prompts the user to enter the amount to complete the order.

Main Method:

Creates an instance of ECommerceStore.

Displays available items.

Enters a loop where the user can add products to the cart by entering the product number or proceed to checkout by entering 0.

If the input is 0, it calls the checkout method and exits the loop.

Closes the scanner at the end.


