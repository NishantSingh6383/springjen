@RestController
@RequestMapping("/users")
public class UserController {

   @Autowired
   private UserService userService;

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
