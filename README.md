package jfsd;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class UserService {

   @Autowired
   private UserRepository userRepository;

   public User getUserById(Long userId) {
      return userRepository.findById(userId).orElse(null);
   }
   
   public User saveUser(User user) {
      return userRepository.save(user);
   }

   public User registerUser(User user) {
      return userRepository.save(user);
   }

   public boolean authenticateUser(User user) {
      User storedUser = userRepository.findByUsername(user.getUsername());
      if (storedUser != null && storedUser.getPassword().equals(user.getPassword())) {
         return true; // Authentication successful
      } else {
         return false; // Authentication failed
      }
   }
}













package jfsd;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

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
      if (userService.authenticateUser(user)) {
         return ResponseEntity.ok("User logged in successfully");
      } else {
         return ResponseEntity.status(HttpStatus.UNAUTHORIZED).body("Invalid credentials");
      }
   }

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
