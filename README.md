import java.util.ArrayList;
import java.util.Scanner;

class MenuItem {
    String name;
    double price;

    MenuItem(String name, double price) {
        this.name = name;
        this.price = price;
    }
}

class Order {
    ArrayList<MenuItem> items = new ArrayList<>();

    void addItem(MenuItem item) {
        items.add(item);
    }

    double calculateTotal() {
        double total = 0;
        for (MenuItem item : items) {
            total += item.price;
        }
        return total;
    }
}

class Restaurant {
    ArrayList<MenuItem> menu = new ArrayList<>();

    void addToMenu(MenuItem item) {
        menu.add(item);
    }
}

public class RestaurantManagementSystem {
    public static void main(String[] args) {
        Restaurant restaurant = new Restaurant();
        Scanner scanner = new Scanner(System.in);

        // Populate the menu
        restaurant.addToMenu(new MenuItem("Burger", 5.99));
        restaurant.addToMenu(new MenuItem("Pizza", 8.99));
        // Add more menu items as needed

        Order order = new Order();

        while (true) {
            // Display menu
            System.out.println("Menu:");
            for (int i = 0; i < restaurant.menu.size(); i++) {
                MenuItem menuItem = restaurant.menu.get(i);
                System.out.println((i + 1) + ". " + menuItem.name + " - $" + menuItem.price);
            }

            // Take user input for order
            System.out.print("Enter the item number to add to your order (0 to finish): ");
            int choice = scanner.nextInt();

            if (choice == 0) {
                break;
            }

            if (choice > 0 && choice <= restaurant.menu.size()) {
                MenuItem selectedMenuItem = restaurant.menu.get(choice - 1);
                order.addItem(selectedMenuItem);
                System.out.println(selectedMenuItem.name + " added to your order.");
            } else {
                System.out.println("Invalid choice. Please try again.");
            }
        }

        // Display order and total
        System.out.println("\nYour Order:");
        for (MenuItem item : order.items) {
            System.out.println("- " + item.name + " - $" + item.price);
        }
        System.out.println("Total: $" + order.calculateTotal());

        scanner.close();
    }
}
