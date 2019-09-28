# springboot-joins


    
   ## Join tables
   ### One to Many
   - the **owning** side
        - usually the "one" side
        - use the `@JoinColumn` to declare the join column name (usually the foreign key in the parent
            ```
            joinColumns = {@JoinColumn(name = "user_id")}
            ```
        - can also create an inverse join column (usually the foreign key in the child), 
            - ` inverseJoinColumns = @JoinColumn(name = "course_id"))`
    
 - the **inverse/referencing**
      - usually the "many" side with the foreign key
      - use `mappedBy`, the value is the name of the entity on the owning side
        ```
        @OneToMany(fetch = FetchType.LAZY, mappedBy = "employee")
        private List<Email> emails;
        ```
 ### Many to Many
 -  https://www.baeldung.com/jpa-many-to-many
 - have each side declare the many to many relations, with the corresponding entity as a property
   ```
    @ManyToMany
    Set<Student> likes;
    
    @ManyToMany
    Set<Student> likes;
     ```
 - configure the relationship
    - in the **owning side** only
        - include the table name 
        - specify the foreing keys for the join columns, and inverse join columns
               - *note*: note this is optional, but recommended if you want  control over the nameing conventions.
            ```
            @ManyToMany
            @JoinTable(
              name = "course_like", 
              joinColumns = @JoinColumn(name = "student_id"), 
              inverseJoinColumns = @JoinColumn(name = "course_id"))
            Set<Course> likedCourses;
            ```
    - in the **target side** map the relationship with `mapped by`
        ```
        @ManyToMany(mappedBy = "likedCourses")
        Set<Student> likes;

        ```




       - specify the column property that will be joined 
       - delcare the **join type**, with the fetch and cascade types specified as arguements
       ```
       private List<Course> courses;
       ```
   
   ### Types
   - **FetchType**
        - .LAZY: (default) Lazy loading - loads only the relationships specified via the getter, can produce NULL pointers
        - .EAGER: loads ALL relationships related to the entity
        
   - **cascadeTypes**: when we perform some action on the target entity, the same action will be applied to the associated entity
        - ALL: propogates ALL operations from parent to child
        - PERSIST: propogates the PERSIST operation from parent to child, when we save the parent, the address will get saved
        - MERGE: propogates the MERGE operatin from the parent to the child
        - REMOVE: propogates the REMOVE operation from parent to child, when we delete the parent, the child will also be   deleted
        - REFRESH: whenever the parent gets reloaded from the DB, so does the child
        - DETACH: when the parent gets removed from the persistent context, so does the child


          
      


      
         

    
      

    
    


    
    
    
  
