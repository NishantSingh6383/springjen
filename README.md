@PostMapping("/register")
public ResponseEntity<String> registerUser(@RequestBody User user) {
   // Implement the logic for user registration
   // Call the corresponding UserService method to register the user
   userService.registerUser(user);
   return ResponseEntity.ok("User registered successfully");
}
