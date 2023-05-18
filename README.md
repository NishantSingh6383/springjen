package jfsd;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;
import jfsd.User;
import jfsd.UserService;
import java.util.List;

@RestController
@RequestMapping("/users")
public class UserController {
	
	
	 @Autowired
	    private UserService userService;
	    
	    @Autowired
	    private MedicineService medicineService;
	    
	    @Autowired
	    private OrderService orderService;

	    @PostMapping("/register")
	    public User registerUser(@RequestBody User user) {
	        return userService.registerUser(user);
	    }

	    @PostMapping("/login")
	    public ResponseEntity<String> loginUser(@RequestBody User user) {
	        // Implementation for user login
	    }

	    @GetMapping("/medicines")
	    public List<Medicine> getMedicines() {
	        return medicineService.getAllMedicines();
	    }

	    @PostMapping("/orders")
	    public ResponseEntity<Order> createOrder(@RequestBody Order order) {
	        Order createdOrder = orderService.createOrder(order);
	        if (createdOrder != null) {
	            return ResponseEntity.ok(createdOrder);
	        } else {
	            return ResponseEntity.status(HttpStatus.BAD_REQUEST).build();
	        }
	    }

	    // Other API endpoints for getting user orders, updating profile, etc.

   

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


