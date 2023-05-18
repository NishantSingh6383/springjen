
User storedUser = userRepository.findByUsername(user.getUsername());
      if (storedUser != null && storedUser.getPassword().equals(user.getPassword())) {
         return true; // Authentication successful
      } else {
         return false; // Authentication failed
      }
      
- The method getUsername() is undefined for the type User
	- userRepository cannot be resolved

- The method getPassword() is undefined for the type User
	- The method getPassword() is undefined for the type User
