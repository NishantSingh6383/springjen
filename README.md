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
}
