import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

public class WebScraper {

    public static void main(String[] args) throws IOException {

        // Replace with the actual URL of the e-commerce website you want to scrape
        String url = "https://www.example.com"; 

        // Create a list to store product information
        List<Product> products = new ArrayList<>();

        // Connect to the website and get the HTML content
        Document doc = Jsoup.connect(url).get();

        // Find all product elements (adjust the CSS selector based on the website's structure)
        Elements productElements = doc.select("div.product"); 

        // Iterate through each product element
        for (Element productElement : productElements) {
            
            // Extract product information (adjust the CSS selectors based on the website's structure)
            String productName = productElement.select("h3.product-name").text();
            String productPrice = productElement.select("span.price").text();
            String productRating = productElement.select("span.rating").text(); 

            // Create a Product object and add it to the list
            Product product = new Product(productName, productPrice, productRating);
            products.add(product);
        }

        // Save product information to a CSV file
        saveToCSV(products, "products.csv");

        System.out.println("Web scraping completed. Data saved to products.csv");
    }

    // Method to save product information to a CSV file
    private static void saveToCSV(List<Product> products, String fileName) throws IOException {
        FileWriter csvWriter = new FileWriter(fileName);
        csvWriter.append("Product Name,Price,Rating\n"); 

        for (Product product : products) {
            csvWriter.append(product.getProductName()).append(",");
            csvWriter.append(product.getProductPrice()).append(",");
            csvWriter.append(product.getProductRating()).append("\n");
        }

        csvWriter. flush();
        csvWriter.close();
    }
}

// Product class to hold product information
class Product {
    private String productName;
    private String productPrice;
    private String productRating;

    public Product(String productName, String productPrice, String productRating) {
        this.productName = productName;
        this.productPrice = productPrice;
        this.productRating = productRating;
    }

    public String getProductName() {
        return productName;
    }

    public String getProductPrice() {
        return productPrice;
    }

    public String getProductRating() {
        return productRating;
    }
} ```java
// Additional functionality to handle exceptions and improve user experience
import java.util.Scanner;

public class EnhancedWebScraper {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the URL of the e-commerce website: ");
        String url = scanner.nextLine();

        try {
            // Create a list to store product information
            List<Product> products = new ArrayList<>();

            // Connect to the website and get the HTML content
            Document doc = Jsoup.connect(url).get();

            // Find all product elements
            Elements productElements = doc.select("div.product");

            // Iterate through each product element
            for (Element productElement : productElements) {
                String productName = productElement.select("h3.product-name").text();
                String productPrice = productElement.select("span.price").text();
                String productRating = productElement.select("span.rating").text();

                // Create a Product object and add it to the list
                Product product = new Product(productName, productPrice, productRating);
                products.add(product);
            }

            // Save product information to a CSV file
            saveToCSV(products, "products.csv");
            System.out.println("Web scraping completed. Data saved to products.csv");

        } catch (IOException e) {
            System.err.println("Error occurred while connecting to the website: " + e.getMessage());
        } finally {
            scanner.close();
        }
    }

    // Method to save product information to a CSV file
    private static void saveToCSV(List<Product> products, String fileName) throws IOException {
        FileWriter csvWriter = new FileWriter(fileName);
        csvWriter.append("Product Name,Price,Rating\n");

        for (Product product : products) {
            csvWriter.append(product.getProductName()).append(",");
            csvWriter.append(product.getProductPrice()).append(",");
            csvWriter.append(product.getProductRating()).append("\n");
        }

        csvWriter.flush();
        csvWriter.close();
    }
}
``` ```java
// Additional class to handle user input and output formatting
import java.util.List;

public class UserInterface {

    public static void displayProducts(List<Product> products) {
        System.out.println("Product List:");
        for (Product product : products) {
            System.out.println("Name: " + product.getProductName());
            System.out.println("Price: " + product.getProductPrice());
            System.out.println("Rating: " + product.getProductRating());
            System.out.println("---------------------------");
        }
    }
}
