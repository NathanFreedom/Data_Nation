# 1st Individual Dart Project

## Project Overview
This project is to conduct an individual practice project
for the simple programming of implementing 4 shopping mall functions
* Period of Time: 30/10/24(Wed) - 31/10/24(Thurs)

## Designed Functions
* F1. To open up the list of the selling products
* F2. To put a product in the shopping cart
* F3. To view the total price of products in the shopping cart
* F4. To close the shopping mall program

## Trouble Shooting & Improvement
* Issue Description: absence of pubspec.yaml 
* Temporary Response: creation of pubspec.ymal file
* Error: actual code emptiness of the file
* Solution: writing customized pubspec.ymal code 
* Future Plan: initially creating a pubspec.ymal file and writing the following code 


## Execution Code

    > import 'dart:io';

    class Product {
      String name;
      int price;
      Product(this.name, this.price);
    }


    class ShoppingMall {
      List<Product> cart = [];
      int totalPrice = 0;

      void addProduct(Product product, int quantity) {
        if (quantity <= 0) {
          print("0개보다 많은 개수의 상품만 담을 수 있어요 !");
          return;
        }
        for (int i = 0; i < quantity; i++) {
          cart.add(product);
          totalPrice += product.price;
        }
      }

      int getTotalPrice() {
        return totalPrice;
      }
    }

    void showProducts(List<Product> products) {
      print("상품 목록:");
      for (var product in products) {
        print("${product.name} / ${product.price}원");
      }
    }

    void main() {
      List<Product> products = [
        Product("셔츠", 45000),
        Product("원피스", 30000),
        Product("반팔티", 35000),
        Product("반바지", 38000),
        Product("양말", 5000)
      ];
      ShoppingMall cart = ShoppingMall();
      bool isRunning = true;
      print("프로그램이 시작되었습니다. 콘솔을 통해 명령을 수행하세요.");
      while (isRunning) {
        print("\n[1] 상품 목록 보기 / [2] 장바구니에 담기 / [3] 장바구니 총 가격 보기 / [4] 프로그램 종료");
          String? input = stdin.readLineSync();

    if (input != null && input.isNotEmpty) {
      if (input == '1') {
        print("상품 목록을 보여드립니다.");
        showProducts(products);
      } else if (input == '2') {
        print("상품 이름을 입력해 주세요:");
        String? productName = stdin.readLineSync();
        print("상품 개수를 입력해 주세요:");
        String? quantityInput = stdin.readLineSync();

    if (productName == null ||
            productName.isEmpty ||
            quantityInput == null ||
            quantityInput.isEmpty) {
          print("입력값이 올바르지 않아요 !");
          continue;
        }

        int quantity;
        try {
          quantity = int.parse(quantityInput);
        } catch (e) {
          print("입력값이 올바르지 않아요 !");
          continue;
        }

        var product = products.firstWhere(
          (p) => p.name == productName,
          orElse: () => Product('', 0),
        );

        if (product.name.isEmpty) {
          print("입력값이 올바르지 않아요 !");
        } else {
          cart.addProduct(product, quantity);
          print("장바구니에 상품이 담겼어요 !");
        }
      } else if (input == '3') {
        print("장바구니에 ${cart.getTotalPrice()}원 어치를 담으셨네요 !");
      } else if (input == '4') {
        print("이용해 주셔서 감사합니다 ~ 안녕히 가세요 !");
        isRunning = false;
        
      } else {
        print("지원하지 않는 기능입니다! 다시 시도해 주세요. (입력값: \"$input\")");
      }
    } else {
      print("올바른 입력값을 제공해 주세요.");
    }
  }
}
