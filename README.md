@PostMapping("/login")
public ResponseEntity<String> loginUser(@RequestBody User user) {
   // Implement the logic for user login
   // Call the corresponding UserService method to authenticate the user
   // Return an appropriate response, such as a success message or an error message

   // Example implementation
   if (userService.authenticateUser(user)) {
      return ResponseEntity.ok("User logged in successfully");
   } else {
      return ResponseEntity.status(HttpStatus.UNAUTHORIZED).body("Invalid credentials");
   }
}
