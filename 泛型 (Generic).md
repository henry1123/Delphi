## 泛型 (Generic)

### Delphi 2009 之後加入

sample code from Dennies Chang - http://firemonkeylessons.blogspot.com/2018/06/delphi-generic.html:
```delphi
TMyStack<T> = class (TObject)
private
   FElements: TArray<T>;
   FElementCount: integer;
public
   function push(element: T) : integer;
   function pop: T;

   property count: integer; read FElementCount;

   constructor Create(); ovevrride; reintroduce;
   destructor Destory(); override;
end;

constructor TMyStack<T>.Create();
begin
   inherited Create();

  FElementCount := 0; 
  setLength(FElements, 0); 
end;

function TMyStack<T>.push(element: T) : integer;
begin
   Inc(self.FElementCount); 
   setLength(FElements, self.FElementCount);

   self.FElements[self.FElementCount -1] := element;
end;

function TMyStack<T>.pop: T;
begin
    Result := self.FElements[self.FElementCount -1];

    Dec(self.FElementCount);
    setLength(FElements, self.FElementCount);
end;

'-----------------------------------------------------

var
   integerStack : TMyStack<Integer>;
begin
    integerStack := TMyStack<Integer>.Create;
    try
        integerStack.push(79);
        integerStack.push(7);
        integerStack.push(21);
        integerStack.push(13); 
    finally
         integerStack.Free;
    end;
end; 

var
   stringStack : TMyStack<String>;
begin
    stringStack := TMyStack<String>.Create;
    try
        stringStack.push('這');
        stringStack.push('就');
        stringStack.push('是');
        stringStack.push('泛'); 
        stringStack.push('型');  
        stringStack.push('啊');  
    finally
         stringStack.Free;
    end;
end;


```
