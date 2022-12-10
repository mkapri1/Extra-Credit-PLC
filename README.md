# Extra-Credit-PLC
## **Specification Document**

### Keyword List
  |Keyword| Representation|
  |-------|-------|
  |IF| $|
  |ELSE| &|
  |BEGIN| #|
  |END| @|
  |Declaration| varie|

  | | |
  |--|--|
  |Addition| + |
  |Subraction| -|
  |Multiplication| *|
  |Division| /|
  |Modulus| %|
  |Left Paren| ( |
  |Right Paren| )|
  |End of Statement| ;|
  |Greater than| >|
  |Less than| < |
  |Greater than equal to| ~|
  |Less than equal to| ^ |
  |Equal| ==|
  |Not Equal| != |
  |Assignment| = |
  
  Boolean -> Yes and No
  
### Grammar
  ````
  <program> --> `#`<stmt_list>`@`
  <stmt_list> --> { <stmt>`;`}
  <stmt> --> <if_stmt> | <while_loop> | <assignment> | <block> |  <declare> 
  <if_stmt> --> `$` `(`<bool_expr> `)` <stmt> [`&` <stmt>]
  <while_loop> --> `ROF` `(` <bool_expr> `)` <stmt>
  <assignment> --> `id` `=` <expr> `;`
  <block> --> `{`<stmt_list>`}`
  <declare> --> `varie` `id` `;`
  <expr> --> <term> {(`*`|`/`|`%`)} <term>
  <term> -->  <factor> {(`+`|`-`)} <factor>
  <factor> --> `id`| `int_lit`| `(`<expr>`)`

  <bool_expr> --> <rel> {(`!=`|`==`)} <rel>
  <rel> --> <bex> {(`<`|`>`|`~`|`^`)} <bex>
  <bex> --> <bterm> {(`*`|`/`|`%`)} <bterm>
  <bterm> --> <bfactor> {(`+`|`-`)} <bfactor>
  <bfactor> --> `id`|`int_lit`|`bool_lit`|`(`<bex>`)`

```` 

### Semantics
IF-ELSE:
````
 <if_stmt> -> $(<bool_expr>) <stmt> [ & <stmt>m ]
 
 M_if(if (bool_expr) <stmt>, s) -->
    
    if M_b(<bool_expr>, s) == error
      return error
    
    if M_b (<bool_expr>,s) 
       if M_stmt(<stmt>,s) == error
          return error
       return M_stmt(<stmt>,s)
       
 M_if($ (bool_expr) <stmt1>, & <stmt2>, s) -->
    
     if M_b(<bool_expr>, s) == error
      return error
     
     if M_b (<bool_expr>,s) 
       if M_stmt(<stmt1>,s) == error
          return error
       return M_stmt(<stmt1>,s)
       
     else
        if M_stmt(<stmt2>,s) == error
          return error
        return M_stmt(<stmt2>,s)
        
````
WHILE:
````
  <while_stmt> --> ROF ( <bool_expr> ) <stmt>
  
  M_while(ROF (bool_expr) <stmt>, s) -->
    
    if M_b(<bool_expr>, s) == error
      return error
    
    if M_b (<bool_expr>,s) 
       if M_stmt(<stmt>,s) == error
          return error
       return M_stmt(<stmt>,s)
````
ASSIGNMENT:
````
  <assignment> --> `id` `=` <expr> `;`
  
  M_assign( id  <expr>, s) -->
    if M_op(=, s) == error
      return error
    if M_op(=,s)
      if M_expr(<expr> , s) == error
        return error
      return M_expr(<expr>,s)
      
      if M_e( ;,s) == error
        return error
      return M_e(;,s)
  
````
BLOCK:
````
  <block> --> { <stmt_list> }
  
  M_block( { <stmt_list> } ,s ) -->
    if M_s ( {, s) == error
      return error
    if M_s( {,s)
      if M_stmtList (<stmt_list> ,s) == error
        return error
      return M_stmtList(<stmt_list>,s)
      
      if M_e( },s) == error
        return error
      return M_e(},s)
     

````
DECLARE:
````
 <declare> --> varie id ;
 
  M_declare(varie id, s) -->
    if M_var( varie,s) == error
      return error
    if M_var( varie,s)
      if M_id( id,s) == error
        return error
      return M_id(id,s)
      
      if M_c( ;,s) == error
        return error
      return M_c(;,s)
      
 ````

    
  
