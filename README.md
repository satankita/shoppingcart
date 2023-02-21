# shoppingcart
// main class for shopping cart program that asks users to fill their cart from a product list








public static void main(String[] args) throws FileNotFoundException {
		
		//import scanner
		Scanner in = new Scanner(System.in);
		
		//ask user for input
		System.out.print("Enter an input file: ");
		String fileName = in.nextLine();
		
		//get list of products from user inputted file 
		List<Product> itemList= loadProductsFromFile(fileName);    	
		
		//displayChoices using method
		displayChoices(itemList);
		
		//initialize new map and list
		HashMap<Product, Integer> map = new HashMap<>();
		List<Product> cartList= new ArrayList<Product>();
		System.out.println();
		
		//ask the user what they want to add
		System.out.print("Enter something to add to the cart (0 to quit): ");
		int itemChoice = Integer.parseInt(in.nextLine());
		
		//ask the user to enter a quantity
		System.out.print("Enter a quantity: ");
		int quantity = Integer.parseInt(in.nextLine());
		
		//add the user input to the cartList
		cartList.add(itemList.get(itemChoice-1));
		
		//make a new list to store quantities
		List<Integer> quantityList = new ArrayList<Integer>();
		quantityList.add(quantity);
		
		//send cartList and quantityList to fill map to get map products and quantities that the user requested
		map = fillMap(cartList, quantityList);
	
		
		System.out.println();
		//diplay the cart
		System.out.println("Your cart contains: ");
		displayCart(map);
		System.out.println();
		
		//continue only when the user hits enter
		System.out.print("Hit ENTER to continue");
		in.nextLine();
		
		//display choices to user again
		displayChoices(itemList);
		System.out.println();
		
		//see if the user would like to add more to the cart
		System.out.print("Enter something to add to the cart (0 to quit): ");
		itemChoice = Integer.parseInt(in.nextLine());
		
		//loop while the user would still like to add more to the cart
		while (itemChoice != 0) {
			
			//ask the user to enter a new quantity
			System.out.print("Enter a quantity: ");
			quantity = Integer.parseInt(in.nextLine());
			
			//add new inputs to the corresponding lists
			quantityList.add(quantity);		
			cartList.add(itemList.get(itemChoice-1));
			
			//fill map with new inputs
			map = fillMap(cartList, quantityList);
			System.out.println();
			//display cart
			System.out.println("Your cart contains: ");
			displayCart(map);
			System.out.println();
			
			//continue only when the user hits enter
			System.out.print("Hit ENTER to continue");
			in.nextLine();
		
			//display choices
			displayChoices(itemList);
			System.out.println();
			
			//ask the user if they would like to continue
			System.out.print("Enter items into the cart (0 to quit): ");
			itemChoice = Integer.parseInt(in.nextLine());
		}
		
		//formatting
		System.out.println();
		
		//display final cart
		System.out.println("Final purchases: ");
		displayCart(map);
		
		
		//close scanner
		in.close();
	}
