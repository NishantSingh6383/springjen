 public Medicine getMedicineById(Long medicineId) {
      return medicineRepository.findById(medicineId).orElse(null);
   }


