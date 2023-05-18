import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;
import com.example.jfsd.User;
import com.example.jfsd.UserService;


@RestController
@RequestMapping("/users")
public class UserController {

   @Autowired
   private UserService userService;

   // Implement your API endpoints here
   
}





@PostMapping("/register")
public User registerUser(@RequestBody User user) {
   // Implement the logic for user registration
   // Call the corresponding UserService method to register the user
   // Return the registered user object or a response message
}
