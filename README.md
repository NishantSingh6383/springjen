@Entity
public class User {

   @Id
   @GeneratedValue(strategy = GenerationType.IDENTITY)
   private Long id;
   
   private String name;
   private String address;
   
   // Getters and setters
   
   // Other properties and methods
}
