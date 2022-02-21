package application;

import java.util.ArrayList;
import java.util.List;
import java.util.Locale;

import model.entities.Product;
import model.services.ProductService;

public class Program {
	
	public static void main(String[] args) {

		Locale.setDefault(Locale.US);
		List<Product> list = new ArrayList<>();

		list.add(new Product("Tv", 900.00));
		list.add(new Product("Mouse", 50.00));
		list.add(new Product("Tablet", 350.50));
		list.add(new Product("HD Case", 80.90));

		ProductService ps = new ProductService();
		
		double sum = ps.filteredSum(list, p -> p.getName().charAt(0) == 'T');
		/*
		 * eu vou chamar o filteredSum passando a lista, e tambem um predicado pra dizer como eu quero filtar minha
		 * lista, no caso aqui eu vou passar a expressão lambda...
		 * p que leva a p.getName().charAt(0) == 'T');
		 */
 
		System.out.println("Sum = " + String.format("%.2f", sum));
	}
}

===========================================================================

package model.entities;

public class Product {

	private String name;
	private Double price;
	
	public Product(String name, Double price) {
		this.name = name;
		this.price = price;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public Double getPrice() {
		return price;
	}
 
	public void setPrice(Double price) {
		this.price = price;
	}

	@Override
	public String toString() {
		return name + ", " + String.format("%.2f", price);
	}
}

===========================================================================

package model.services;

import java.util.List;
import java.util.function.Predicate;

import model.entities.Product;

public class ProductService {

	public double filteredSum(List<Product> list, Predicate<Product> criteria) {
		/*
		 * eu vou receber a condição aqui, que é o predicate, e vou aplicar a condição no if, 
		 */
		double sum = 0.0;
		for (Product p : list) {
			if (criteria.test(p)) {
				/*
				 * aqui eu coloco a chamada do metodo do predicado, que vai ser criteria.test(p);, então aqui eu to
				 * fazendo um test generico de qualquer predicado que for recebido aqui como parametro. 
				 */
				sum += p.getPrice();
			}
		}
		return sum;
	}
}

