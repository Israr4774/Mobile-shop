# Mobile-shop



import java.util.ArrayList;
import java.util.List;

public class MobileShop {
    private String name;
    private List<Mobile> mobiles;
    private List<Purchase> purchases;

    public MobileShop(String name) {
        this.name = name;
        this.mobiles = new ArrayList<>();
        this.purchases = new ArrayList<>();
    }

    public void addMobile(Mobile mobile) {
        mobiles.add(mobile);
    }

    public void displayMobiles() {
        System.out.println(name + " Inventory:");
        for (Mobile mobile : mobiles) {
            mobile.displayDetails();
        }
    }

    public void purchaseMobile(Customer customer, int mobileId, int quantity) {
        for (Mobile mobile : mobiles) {
            if (mobile.getId() == mobileId && mobile.getStock() >= quantity) {
                mobile.setStock(mobile.getStock() - quantity);
                Purchase purchase = new Purchase(purchases.size() + 1, customer, mobile, quantity);
                purchases.add(purchase);
                System.out.println("Purchase successful!");
                purchase.displayDetails();
                return;
            }
        }
        System.out.println("Purchase failed: Mobile not found or insufficient stock.");
    }

    public static void main(String[] args) {
        MobileShop shop = new MobileShop("Israr Mobile Shop");

        Mobile mobile1 = new Mobile(1, "Apple", "iPhone 13", 999.99, 10);
        Mobile mobile2 = new Mobile(2, "Samsung", "Galaxy S21", 799.99, 15);
        Mobile mobile3 = new Mobile(3, "OnePlus", "9 Pro", 969.99, 5);

        shop.addMobile(mobile1);
        shop.addMobile(mobile2);
        shop.addMobile(mobile3);

        shop.displayMobiles();

        Customer customer1 = new Customer(1, "John Doe", "john@example.com");
        Customer customer2 = new Customer(2, "Jane Smith", "jane@example.com");

        shop.purchaseMobile(customer1, 1, 2);
        shop.purchaseMobile(customer2, 2, 1);

        shop.displayMobiles();
    }
}
