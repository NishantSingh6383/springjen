
User storedUser = userRepository.findByUsername(user.getUsername());
      if (storedUser != null && storedUser.getPassword().equals(user.getPassword())) {
         return true; // Authentication successful
      } else {
         return false; // Authentication failed
      }
      
