
package jfsd;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;
import jfsd.User;
import jfsd.UserService;


@RestController
@RequestMapping("/users")
public class UserController {

   @Autowired
   private UserService userService;

   @PostMapping("/register")
   public User registerUser(@RequestBody User user) {
      // Call the registerUser method from the userService
      return userService.registerUser(user);
   }

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
   
  
   @PostMapping("/register")
   public ResponseEntity registerUser(@RequestBody User user) { 
	   User registeredUser = userService.registerUser(user); 
	   if (registeredUser != null) { 
		   return ResponseEntity.ok(registeredUser);
		   } 
	   else { return ResponseEntity.badRequest().body(null); } }
   
// Other API endpoints
   
   @GetMapping("/{userId}/profile")
   public ResponseEntity<User> getUserProfile(@PathVariable Long userId) {
      User user = userService.getUserById(userId);
      if (user != null) {
         return ResponseEntity.ok(user);
      } else {
         return ResponseEntity.notFound().build();
      }
   }

   @PutMapping("/{userId}/profile")
   public ResponseEntity<User> updateUserProfile(@PathVariable Long userId, @RequestBody User updatedUser) {
      User user = userService.getUserById(userId);
      if (user != null) {
         user.setName(updatedUser.getName());
         user.setAddress(updatedUser.getAddress());
         // Set other profile properties
         User savedUser = userService.saveUser(user);
         return ResponseEntity.ok(savedUser);
      } else {
         return ResponseEntity.notFound().build();
      }
   }

   
   
}
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	package jfsd;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;
import jfsd.User;
import jfsd.UserService;

@RestController
@RequestMapping("/users")
public class UserController {

   @Autowired
   private UserService userService;

   @PostMapping("/register")
   public ResponseEntity<User> registerUser(@RequestBody User user) {
      User registeredUser = userService.registerUser(user);
      if (registeredUser != null) {
         return ResponseEntity.ok(registeredUser);
      } else {
         return ResponseEntity.badRequest().body(null);
      }
   }

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
   
   // Other API endpoints
   
   @GetMapping("/{userId}/profile")
   public ResponseEntity<User> getUserProfile(@PathVariable Long userId) {
      User user = userService.getUserById(userId);
      if (user != null) {
         return ResponseEntity.ok(user);
      } else {
         return ResponseEntity.notFound().build();
      }
   }

   @PutMapping("/{userId}/profile")
   public ResponseEntity<User> updateUserProfile(@PathVariable Long userId, @RequestBody User updatedUser) {
      User user = userService.getUserById(userId);
      if (user != null) {
         user.setName(updatedUser.getName());
         user.setAddress(updatedUser.getAddress());
         // Set other profile properties
         User savedUser = userService.saveUser(user);
         return ResponseEntity.ok(savedUser);
      } else {
         return ResponseEntity.notFound().build();
      }
   }
}

