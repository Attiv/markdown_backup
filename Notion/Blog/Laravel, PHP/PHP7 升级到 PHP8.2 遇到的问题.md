- `PHP Deprecated: Function libxml_disable_entity_loader() is deprecated`
    - 删除所有 `libxml_disable_entity_loader` 代码
- `strtoupper(): Passing null to parameter \#1 ($string) of type string is deprecated`
    - 参数为空是添加个对应类型的默认值
- `PHP Deprecated: Return type of xxx should either be compatible with IteratorAggregate::getIterator(): Traversable, or the #[\ReturnTypeWillChange] attribute should be used to temporarily suppress the notice`
    - 函数上面加上 `#[\ReturnTypeWillChange]`
- `implements the Serializable interface, which is deprecated. Implement __serialize() and __unserialize() instead (or in addition, if support for old PHP versions is necessary)`
    
    - 加上
    
    ```Dart
    public function __serialize() {}
    public function __unserialize(array $data): void {}
    ```
    
- `PHP Deprecated: Optional parameter $defaultProvider declared before required parameter`
    - 最简单的做法是给 required 参数个默认值变成可选
- `Uncaught Symfony\Component\Debug\Exception\FatalThrowableError: Class "Predis\Profile\Factory" not found`
    - 使用 `use Predis\Profile` 代替 `Predis\Profile\Factory`
- `PHP Deprecated: Creation of dynamic property xxx is deprecated`
    
    ```Dart
    use AllowDynamicProperties;
    
    #[AllowDynamicProperties]
    class MyApiClient extends ApiClient { }
    ```
    
- `getClass() is deprecated`
    
    - 需要根据代码逻辑修改，比如
    
    ```Dart
     // $name = $reflectionParam->getClass();
     $name = $param->getType() && !$param->getType()->isBuiltin() 
       ? new ReflectionClass($param->getType()->getName())
       : null;
    ```