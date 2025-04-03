package com.LMS;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class LmsApplication {
    public static void main(String[] args) {
        SpringApplication.run(LmsApplication.class, args);
    }
} 

// User Entity
package com.lms.model;

import jakarta.persistence.*;

@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;
    private String role; // ADMIN, INSTRUCTOR, STUDENT
    
    // Getters and Setters
}

// Course Entity
package com.lms.model;

import jakarta.persistence.*;

@Entity
@Table(name = "courses")
public class Course {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String title;
    private String description;
    private Long instructor;
    
    // Getters and Setters
}

// Enrollment Entity
package com.lms.model;

import Jakarta.persistence.*;

@Entity
@Table(name = "enrollments")
public class Enrollment {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private Long student;
    private Long course;
    
    // Getters and Setters
}

// User Repository
package com.lms.repository;

import com.lms.model.User;
import org. spring. framework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
}

// Course Repository
package com.lms.repository;

import com.lms.model.Course;
import org.springframework.data.jpa.repository.JpaRepository;

public interface CourseRepository extends JpaRepository<Course, Long> {
}

// Enrollment Repository
package com.lms.repository;

import com.lms.model.Enrollment;
import org. spring framework.data.jpa.repository.JpaRepository;

public interface EnrollmentRepository extends JpaRepository<Enrollment, Long> {
}

// User Controller
package com.lms.controller;

import com.lms.model.User;
import com.lms.repository.UserRepository;
import org. spring. framework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/users")
public class UserController {
    private final UserRepository userRepository;
    
    public UserController(UserRepository user repository) {
        this.userRepository = userRepository;
    }
    
    @GetMapping
    public List<User> getAllUsers() {
        return userRepository.findAll();
    }
    
    @PostMapping
    public User createUser(@RequestBody User user) {
        return userRepository.save(user);
    }
}

// Course Controller
package com.lms.controller;

import com.lms.model.Course;
import com.lms.repository.CourseRepository;
import org. spring. framework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/courses")
public class CourseController {
    private final CourseRepository course repository;
    
    public CourseController(CourseRepository course repository) {
        this.courseR rpository = courseRepository;
    }
    
    @GetMapping
    public List<Course> getAllCourses() {
        return courseRepository.findAll();
    }
    
    @PostMapping
    public Course createCourse(@RequestBody Course course) {
        return courseRepository.save(course);
    }
}

// Enrollment Controller
package com.lms.controller;

import com.lms.model.Enrollment;
import com.lms.repository.EnrollmentRepository;
import org. spring framework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/enrollments")
public class EnrollmentController {
    private final EnrollmentRepository enrollmentRepository;
    
    public EnrollmentController(EnrollmentRepository enrollmentRepository) {
        this.enrollmentRepository = enrollmentRepository;
    }
    
    @GetMapping
    public List<Enrollment> getAllEnrollments() {
        return enrollmentRepository.findAll();
    }
    
    @PostMapping
    public Enrollment enrollStudent(@RequestBody Enrollment enrollment) {
        return enrollmentRepository.save(enrollment);
    }
}
                                
