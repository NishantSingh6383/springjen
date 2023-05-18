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

   // Other API endpoints
   
}
