## Reentrant Lock

![image](https://user-images.githubusercontent.com/28957748/123784810-07442300-d902-11eb-9e89-a1c0a7a5925d.png)

![image](https://user-images.githubusercontent.com/28957748/123784939-2478f180-d902-11eb-9e1e-c5c0a62219a0.png)

![image](https://user-images.githubusercontent.com/28957748/123785082-4d998200-d902-11eb-9d91-0d1a9ff5737d.png)

![image](https://user-images.githubusercontent.com/28957748/123785119-5be79e00-d902-11eb-85c1-b64af8b2e89d.png)

![image](https://user-images.githubusercontent.com/28957748/123785288-8fc2c380-d902-11eb-93b9-25624f977e64.png)

![image](https://user-images.githubusercontent.com/28957748/123785494-cb5d8d80-d902-11eb-8ccf-04b8e870180d.png)

![image](https://user-images.githubusercontent.com/28957748/123785527-d57f8c00-d902-11eb-9b99-60a4b6c86e10.png)

![image](https://user-images.githubusercontent.com/28957748/123785618-f2b45a80-d902-11eb-9c2b-d0a89bd598d8.png)

![image](https://user-images.githubusercontent.com/28957748/123785720-12e41980-d903-11eb-8e4d-76017b4ac6f6.png)

![image](https://user-images.githubusercontent.com/28957748/123785850-30b17e80-d903-11eb-9833-3b754ae0d53a.png)

## LockInterruptibly

![image](https://user-images.githubusercontent.com/28957748/123786088-825a0900-d903-11eb-9db0-a247835c9aac.png)

![image](https://user-images.githubusercontent.com/28957748/123786277-b7fef200-d903-11eb-8af9-3d4a7e423995.png)

![image](https://user-images.githubusercontent.com/28957748/123786342-c947fe80-d903-11eb-9dd9-69df06c4f93f.png)

## Try lock
![image](https://user-images.githubusercontent.com/28957748/123786475-ebda1780-d903-11eb-9c47-9c0901fc3ba7.png)

![image](https://user-images.githubusercontent.com/28957748/123786772-46737380-d904-11eb-8ab6-a5785dc5e58d.png)

![image](https://user-images.githubusercontent.com/28957748/123786804-50957200-d904-11eb-9829-843fe407c715.png)

![image](https://user-images.githubusercontent.com/28957748/123786845-5ee38e00-d904-11eb-99b3-741f1892240a.png)

![image](https://user-images.githubusercontent.com/28957748/123786894-6c991380-d904-11eb-8e7e-5b60d47faa91.png)

![image](https://user-images.githubusercontent.com/28957748/123786938-79b60280-d904-11eb-8bda-603dbf713c66.png)

## Summary

![image](https://user-images.githubusercontent.com/28957748/123787024-8cc8d280-d904-11eb-9ee0-4ef116cc5981.png)

## ReentrantReadWriteLock

![image](https://user-images.githubusercontent.com/28957748/123796462-5775b200-d90f-11eb-954e-677f3066d651.png)

![image](https://user-images.githubusercontent.com/28957748/123796633-8724ba00-d90f-11eb-9830-56f43b9a8129.png)

![image](https://user-images.githubusercontent.com/28957748/123796726-9dcb1100-d90f-11eb-9d5b-776737886843.png)

![image](https://user-images.githubusercontent.com/28957748/123796875-c94dfb80-d90f-11eb-8c57-ac437c4a89a2.png)

![image](https://user-images.githubusercontent.com/28957748/123796913-d539bd80-d90f-11eb-82f6-1c9f34caffb2.png)

![image](https://user-images.githubusercontent.com/28957748/123796992-ed114180-d90f-11eb-8d66-c163a58fef1f.png)

## Readlock
![image](https://user-images.githubusercontent.com/28957748/123799189-25b21a80-d912-11eb-95d5-ce704ce67e3a.png)

## WriteLock
![image](https://user-images.githubusercontent.com/28957748/123799336-52663200-d912-11eb-8907-2afd07702ddf.png)

![image](https://user-images.githubusercontent.com/28957748/123799482-788bd200-d912-11eb-8550-988e8ad3f022.png)

## Summary 
![image](https://user-images.githubusercontent.com/28957748/123800605-aa516880-d913-11eb-86d0-d72f509eaf82.png)

![image](https://user-images.githubusercontent.com/28957748/123800657-b9d0b180-d913-11eb-9efb-2b3de0830a8a.png)

## Use case 1: Financial assets dashboard

![image](https://user-images.githubusercontent.com/28957748/123789055-efbb6900-d906-11eb-85cf-cb14b079ec46.png)

![image](https://user-images.githubusercontent.com/28957748/123789989-01514080-d908-11eb-9dd4-a80bb136b93d.png)

## Use case 2: Inventory
![image](https://user-images.githubusercontent.com/28957748/123799740-b5f05f80-d912-11eb-8810-82cb4378958c.png)

## Use case 3: Product Reviews Service
```java
import java.util.*;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReadWriteLock;
import java.util.concurrent.locks.ReentrantReadWriteLock;

public class ProductReviewsService {
    private final HashMap<Integer, List<String>> productIdToReviews;

    private ReadWriteLock lock = new ReentrantReadWriteLock();
    private Lock readLock = lock.readLock();
    private Lock writeLock = lock.writeLock();

    public ProductReviewsService() {
        this.productIdToReviews = new HashMap<>();
    }

    /**
     * Adds a product ID if not present
     */
    public void addProduct(int productId) {
        Lock lock = getLockForAddProduct();

        lock.lock();

        try {
            if (!productIdToReviews.containsKey(productId)) {
                productIdToReviews.put(productId, new ArrayList<>());
            }
        } finally {
            lock.unlock();
        }
    }

    /**
     * Removes a product by ID if present
     */
    public void removeProduct(int productId) {
        Lock lock = getLockForRemoveProduct();

        lock.lock();

        try {
            if (productIdToReviews.containsKey(productId)) {
                productIdToReviews.remove(productId);
            }
        } finally {
            lock.unlock();
        }
    }

    /**
     * Adds a new review to a product
     * @param productId - existing or new product ID
     * @param review - text containing the product review
     */
    public void addProductReview(int productId, String review) {
        Lock lock = getLockForAddProductReview();

        lock.lock();

        try {
            if (!productIdToReviews.containsKey(productId)) {
                productIdToReviews.put(productId, new ArrayList<>());
            }
            productIdToReviews.get(productId).add(review);
        } finally {
            lock.unlock();
        }
    }

    /**
     * Returns all the reviews for a given product
     */
    public List<String> getAllProductReviews(int productId) {
        Lock lock = getLockForGetAllProductReviews();

        lock.lock();

        try {
            if (productIdToReviews.containsKey(productId)) {
                return Collections.unmodifiableList(productIdToReviews.get(productId));
            }
        } finally {
            lock.unlock();
        }

        return Collections.emptyList();
    }

    /**
     * Returns the latest review for a product by product ID
     */
    public Optional<String> getLatestReview(int productId) {
        Lock lock = getLockForGetLatestReview();

        lock.lock();

        try {

            if (productIdToReviews.containsKey(productId) && !productIdToReviews.get(productId).isEmpty()) {
                List<String> reviews = productIdToReviews.get(productId);
                return Optional.of(reviews.get(reviews.size() - 1));
            }
        } finally {
            lock.unlock();
        }

        return Optional.empty();
    }

    /**
     * Returns all the product IDs that contain reviews
     */
    public Set<Integer> getAllProductIdsWithReviews() {
        Lock lock = getLockForGetAllProductIdsWithReviews();

        lock.lock();

        try {
            Set<Integer> productsWithReviews = new HashSet<>();
            for (Map.Entry<Integer, List<String>> productEntry : productIdToReviews.entrySet()) {
                if (!productEntry.getValue().isEmpty()) {
                    productsWithReviews.add(productEntry.getKey());
                }
            }
            return productsWithReviews;
        } finally {
            lock.unlock();
        }
    }

    Lock getLockForAddProduct() {
        return writeLock;
    }

    Lock getLockForRemoveProduct() {
        return writeLock;
    }

    Lock getLockForAddProductReview() {
        return writeLock;
    }

    Lock getLockForGetAllProductReviews() {
        return readLock;
    }

    Lock getLockForGetLatestReview() {
        return readLock;
    }

    Lock getLockForGetAllProductIdsWithReviews() {
        return readLock;
    }
}

```

## TODO: Code out Use case 1
## TODO2: Code out Use case 2

