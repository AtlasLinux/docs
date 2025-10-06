# libacl
A config library

## Types
* Some opaque types; mirrors internal structure
    ```c
    typedef struct AclValue AclValue;
    typedef struct AclField AclField;
    typedef struct AclBlock AclBlock;
    typedef struct AclError AclError;
    ```
## Functions
* Lifecycle (no-op for now)
    ```c
    int acl_init(void);
    void acl_shutdown(void);
    ```
* Parse from file or in-memory string.  
  Returns a heap-allocated AclBlock* (linked list of top-level blocks) on success,  
  or NULL on failure (in which case an error may have been printed to stderr).
    ```c
    AclBlock *acl_parse_file(const char *path);
    AclBlock *acl_parse_string(const char *text);
    ```
* Resolve references in-place. Returns 1 on success, 0 on failure.
    ```c
    int acl_resolve_all(AclBlock *root);
    ```
* Utilities
    ```c
    void acl_print(AclBlock *root, FILE *out);
    ```
* Free tree returned by parser
    ```c
    void acl_free(AclBlock *root);  
    ```