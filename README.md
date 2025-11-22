# Taran
Scanner sc = new Scanner(System.in);
        PaymentProcessor processor = null;

        while (true) {
            System.out.println("\n===== PAYMENT SYSTEM MENU =====");
            System.out.println("1. Use PayPal");
            System.out.println("2. Use Stripe");
            System.out.println("3. Make Payment");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            int choice = sc.nextInt();

            switch (choice) {
                case 1 -> {
                    processor = new PayPalAdapter(new PayPalAPI());
                    System.out.println("✅ Switched to PayPal payment gateway.");
                }
                case 2 -> {
                    processor = new StripeAdapter(new StripeAPI());
                    System.out.println("✅ Switched to Stripe payment gateway.");
                }
                case 3 -> {
                    if (processor == null) {
                        System.out.println("⚠️ Please select a payment gateway first!");
                    } else {
                        System.out.print("Enter amount to pay (USD): ");
                        double amount = sc.nextDouble();
                        processor.pay(amount);
                    }
                }
                case 4 -> {
                    System.out.println("Thank you for using the Payment System!");
                    sc.close();
                    System.exit(0);
                }
                default -> System.out.println("Invalid choice! Try again.");
            }
        }
