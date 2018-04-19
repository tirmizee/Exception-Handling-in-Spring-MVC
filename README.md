# Exception-Handling-in-Spring-MVC
see : https://spring.io/blog/2013/11/01/exception-handling-in-spring-mvc

1.First Step

	 public class ExceptionNotFound  extends RuntimeException   {
	    private static final long serialVersionUID = -4123180079950070796L;
	 }
2.Step Two

	@ResponseBody
	@RequestMapping(value = "/delete/{id}" , method = RequestMethod.GET, headers = "Accept=application/json")
	public boolean update(@PathVariable Long id)  throws Exception {
		if(id > 0){
			throw new ExceptionNotFound();
		}
		try { userDao.delete(id); } catch (Exception e) { return false; }
		return true;
		
	}
	
	@ResponseBody
	@ExceptionHandler(ExceptionNotFound.class)
	public ResponseEntity<String> handleEmployeeNotFoundException(HttpServletRequest request, Exception ex){
	    return new ResponseEntity<String>("Hello : ",  HttpStatus.CREATED);
	}	
	

