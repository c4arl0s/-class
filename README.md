# @class

The following explanation is written in spanish because is difficult to understand it english language xD

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

Entonces, cuando estas usando la clase, tu puedes crear instancias de la clase, asi tambien, implementar el protocolo con una unica declaracion de importacion.

```objective-c
#import "CustomClass"

@interface AnotherCustomClass()<CustomClassDelegate>

@property (nonatomic, strong) CustomClass *customClass;

end

@implementation AnotherCustomClass

#pragma mark - CustomClassDelegate Protocol Methods

-(void)CustomClassDidSomething:(CustomClass *)customClass
{
  NSLog(@"Custom Class did something!");
}

-(void)customClass:(CustomClass *)customClass didSomethingWithResponse:(NSObject *)response
{
  NSLog(@"Custom Class did something with %@!", response);
}

-(BOOL)shouldCustomClassDoSomething
{
  return YES;
}

-(BOOL)shouldCustomClass:(CustomClass *)customClass doSomethingWithInput:(NSObject *)input
{
  if([input isEqual:YES])
  {
    return YES;
  }
  return NO;
}

-(void)doSomething
{
  self.customClass = [[CustomClass alloc] init];
  self.customClass.delegate = self;
  [self.customClass doSomething];
  
}
```


