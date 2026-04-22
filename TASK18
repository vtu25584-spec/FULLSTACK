package task18;

import org.junit.jupiter.api.Test;
import org.mockito.Mockito;
import org.springframework.web.client.RestTemplate;
import static org.junit.jupiter.api.Assertions.*;

class Product {
    private Long id;
    private String name;
    private double price;

    public Product(Long id, String name, double price) {
        this.id = id;
        this.name = name;
        this.price = price;
    }

    public String getName() { return name; }
}

class ProductService {

    private RestTemplate restTemplate;

    public ProductService(RestTemplate restTemplate) {
        this.restTemplate = restTemplate;
    }

    public Product getProduct(Long id) {
        return restTemplate.getForObject("url/" + id, Product.class);
    }
}

public class Task18Test {

    @Test
    void testServiceSuccess() {
        RestTemplate restTemplate = Mockito.mock(RestTemplate.class);
        ProductService service = new ProductService(restTemplate);

        Product mockProduct = new Product(1L, "Laptop", 50000);

        Mockito.when(restTemplate.getForObject(Mockito.anyString(), Mockito.eq(Product.class)))
                .thenReturn(mockProduct);

        Product result = service.getProduct(1L);

        assertEquals("Laptop", result.getName());
    }

    @Test
    void testServiceFailure() {
        RestTemplate restTemplate = Mockito.mock(RestTemplate.class);
        ProductService service = new ProductService(restTemplate);

        Mockito.when(restTemplate.getForObject(Mockito.anyString(), Mockito.eq(Product.class)))
                .thenThrow(new RuntimeException());

        try {
            service.getProduct(1L);
        } catch (Exception e) {
            assertTrue(true);
        }
    }
}
