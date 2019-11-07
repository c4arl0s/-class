# @class

The following explanation is write it down in spanish because is difficult to understand it english language xD

``` objective-c
@class CustomClass

@protocol CustomClassDelegate<NSObject>

-(void)CustomClassDidSomething:(CustomClass *)customClass;
-(void)customClass:(CustomClass *)customClass didSomethingWithResponse:(NSObject *)response;
-(BOOL)shouldCustomClassDoSomething:(CustomClass *)customClass;
-(BOOL)shouldCustomClass:(CustomClass *)customClass doSomethingWithInput:(NSObject *)input;

@end

// CustomClass aun no se ha definido aún, pero CustomClassDelegate compilara aunque el parametro mencionado customClass no exista.
// la declaracion @class le dice al compilador "apenas viene la clase, no te preocupes"
// Tu no puedes enviar ningun mensaje a CustomClass en una declaracion de protocolo de cualquier forma.
// pero es importante hacer notar que la declaración @class solo te deja referenciar la clase que aun no se ha definido.
// Eso es todo.
// El compilador no sabe nada acerca de CustomClass mas que su definicion vendrá eventualmente.

@interface CustomClass: NSObject

@property (nonatomic, assign) id<CustomClassDelegate> delegate;

-(void)doSomething;
-(void)doSomethingWithInput:(NSObject *)input;

@end
```



