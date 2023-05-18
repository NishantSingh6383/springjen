@PostMapping("/register")
public ResponseEntity<String> registerUser(@RequestBody User user) {
   boolean isRegistered = userService.registerUser(user);
   if (isRegistered) {
      return ResponseEntity.ok("User registered successfully.");
   } else {
      return ResponseEntity.badRequest().body("Failed to register user.");
   }
}

   
   
   public boolean registerUser(User user) {
   // Implement the logic for user registration
   // You can perform validations, save the user to the database, etc.
   // Return true if the registration is successful, false otherwise
}
