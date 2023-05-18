import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import com.example.yourprojectname.User;
import com.example.yourprojectname.UserRepository;


@Service
public class UserService {

   @Autowired
   private UserRepository userRepository;
   
   // Implement your business logic and data manipulation operations here
   
}




@Service
public class MedicineService {

   @Autowired
   private MedicineRepository medicineRepository;
   
   // Implement your business logic and data manipulation operations here
   
}
