import java.util.ArrayList;
import java.util.Scanner;

class Product {
    private String name;
    private double price;

    public Product(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    public String toString() {
        return name + " - $" + price;
    }
}

class ShoppingCart {
    private ArrayList<Product> cartItems;

    public ShoppingCart() {
        cartItems = new ArrayList<>();
    }

    public void addProduct(Product product) {
        cartItems.add(product);
        System.out.println(product.getName() + " added to cart.");
    }

    public void removeProduct(String productName) {
        for (Product product : cartItems) {
            if (product.getName().equalsIgnoreCase(productName)) {
                cartItems.remove(product);
                System.out.println(product.getName() + " removed from cart.");
                return;
            }
        }
        System.out.println("Product not found in cart.");
    }

    public void viewCart() {
        if (cartItems.isEmpty()) {
            System.out.println("Your cart is empty.");
            return;
        }
        System.out.println("Items in your cart:");
        for (Product product : cartItems) {
            System.out.println(product);
        }
        System.out.println("Total: $" + calculateTotal());
    }

    public double calculateTotal() {
        double total = 0;
        for (Product product : cartItems) {
            total += product.getPrice();
        }
        return total;
    }
}

public class ShoppingCartApp {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ShoppingCart cart = new ShoppingCart();

        Product[] storeProducts = {
            new Product("Laptop", 999.99),
            new Product("Phone", 599.99),
            new Product("Headphones", 199.99),
            new Product("Mouse", 49.99)
        };

        while (true) {
            System.out.println("\n--- Shopping Cart Menu ---");
            System.out.println("1. View Products");
            System.out.println("2. Add Product to Cart");
            System.out.println("3. Remove Product from Cart");
            System.out.println("4. View Cart");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");

            int choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {
                case 1:
                    System.out.println("\nAvailable Products:");
                    for (int i = 0; i < storeProducts.length; i++) {
                        System.out.println((i + 1) + ". " + storeProducts[i]);
                    }
                    break;
                case 2:
                    System.out.print("Enter product number to add: ");
                    int addIndex = scanner.nextInt() - 1;
                    if (addIndex >= 0 && addIndex < storeProducts.length) {
                        cart.addProduct(storeProducts[addIndex]);
                    } else {
                        System.out.println("Invalid product number.");
                    }
                    break;
                case 3:
                    System.out.print("Enter product name to remove: ");
                    String removeName = scanner.nextLine();
                    cart.removeProduct(removeName);
                    break;
                case 4:
                    cart.viewCart();
                    break;
                case 5:
                    System.out.println("Thank you for shopping!");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid choice. Try again.");
            }
        }
    }
}
