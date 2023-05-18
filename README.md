@PostMapping("/register")
public ResponseEntity<String> registerUser(@RequestBody User user) {
   boolean isRegistered = userService.registerUser(user);
   if (isRegistered) {
      return ResponseEntity.ok("User registered successfully.");
   } else {
      return ResponseEntity.badRequest().body("Failed to register user.");
   }
}

   
 @PostMapping("/register")
public ResponseEntity<String> registerUser(@RequestBody User user) {
   User registeredUser = userService.registerUser(user);
   if (registeredUser != null) {
      return ResponseEntity.ok("User registered successfully.");
   } else {
      return ResponseEntity.badRequest().body("Failed to register user.");
   }
}
