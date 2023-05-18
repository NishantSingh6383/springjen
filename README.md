@Service
public class UserService {

   @Autowired
   private UserRepository UserRepository;
   
   
   
   public User getUserById(Long userId) {
	   
	   return UserRepository.findById(userId).orElse(null);
	      // Implement logic to retrieve a user by their ID
	      // Use userRepository.findById(userId) to fetch the user from the database
	      // Return the user object if found, or null if not found
	   }
	   
	   public User saveUser(User user) {
		   
		   return UserRepository.save(user);
	      // Implement logic to save/update a user
	      // Use userRepository.save(user) to persist the user in the database
	      // Return the saved user object
	   }
   
   public User registerUser(User user) {
	   
	   
	   return UserRepository.save(user);
   }

   public boolean authenticateUser(User user) {
	   User storedUser = UserRepository.findByUsername(user.getUsername());
	      if (storedUser != null && storedUser.getPassword().equals(user.getPassword())) {
	         return true; // Authentication successful
	      } else {
	         return false; // Authentication failed
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

   
