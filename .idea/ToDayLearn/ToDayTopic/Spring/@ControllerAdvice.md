## @ControllerAdvice 사용 방법


### @ControllerAdvice란?

> @ControllerAdvice란 모든 Controller에서 발생할 수 있는 예외를 잡아 처리해주는 어노테이션입니다.

### @ExceptionHandler란?

> @ExceptionHandler란 @Controller, @RestController 어노테이션이 적용된 Bean 내에서 발생하는 예외를 잡아서 하나의 메서드에서 처리를 해주는 기능입니다.
Contoller, RestController에서만 적용이 가능합니다.(@Service 같은 빈에서는 적용이 안됩니다.)


### 🖊 개요
@ControllerAdvice는 Advice가 이름에 들어있는 걸 보아 AOP의 Advice인듯 하고 클래스를 살펴보면 런타임에 동작하고 @Component가 달려있어서 이 어노테이션을 달면 자동으로 Bean등록이 된다. 역할은 컨트롤러에서 발생하는 예외처리이며 포인트컷 역할로 @ExceptionHandler가 있다. @ExceptionHandler는 메서드를 대상으로 런타임에 동작하며 파라미터로 Throwable 가능한 클래스(Exception 클래스)를 배열로(여러개) 받을 수 있다. 따라서 @ExceptionHandler에 파라미터로 넘긴 여러개의 Exception이 포인트컷의 조건이 되어 지정된 메소드가 동작한다.

### 🖊 사용법
1. Exception을 관리할 클래스에 @ControllerAdvice를 달아준다.


    @ControllerAdvice
        public class CustomExceptionHandler {

        }
2. 해당 클래스에 범위를 지정할 @ExceptionHandler를 메서드에 달아준다.


    @ControllerAdvice
        public class CustomExceptionHandler {
    
        @ExceptionHandler(Exception.class)
        public ResponseEntity<> handleAll(Exception ex){

        }
     }
3. 메서드에 해당 범위에 맞는 Excpetion이 컨트롤러에서 Throw 됐을 때 컨트롤러가 리턴할 값을 지정해준다.
   

    @ControllerAdvice
            public class CustomExceptionHandler {
    
            @ExceptionHandler(Exception.class)
            public ResponseEntity<ErrorResponseEntity> handleAll(Exception ex){
            ErrorResponseEntity response = new ErrorResponseEntity(ErrorCode.INTERNAL_SERVER_ERROR);
    
            return new ResponseEntity<>(response, HttpStatus.INTERNAL_SERVER_ERROR);
            }
        }

---
>**주의사항/알아 둘 것**
>
>Controller, RestController에만 적용가능하다. (@Service같은 빈에서는 안됨.)
> 1. 리턴 타입은 자유롭게 해도 된다. (Controller내부에 있는 메서드들은 여러 타입의 response를 할 것이다. 해당 타입과 전혀다른 리턴 타입이어도 상관없다.)
> 2. @ExceptionHandler를 등록한 Controller에만 적용된다. 다른 Controller에서 NullPointerException이 발생하더라도 예외를 처리할 수 없다.
> 3. 메서드의 파라미터로 Exception을 받아왔는데 이것 또한 자유롭게 받아와도 된다.
