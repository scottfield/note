###getter template
```
#if($field.modifierStatic)
static ##
#end
$field.type ##
#set($name = $StringUtil.capitalizeWithJavaBeanConvention($StringUtil.sanitizeJavaIdentifier($helper.getPropertyName($field, $project))))
#if ($field.boolean && $field.primitive)
is##
#else
get##
#end
#if ($field.boolean || $field.primitive||$field.string)
${name}() {
return $field.name;
}
#else
${name}() {
return Objects.isNull($field.name)? null: ($field.typeName)${field.name}.clone();
}
#end

```
###setter template
```
#set($paramName = $helper.getParamName($field, $project))
#if($field.modifierStatic)
static ##
#end
void set$StringUtil.capitalizeWithJavaBeanConvention($StringUtil.sanitizeJavaIdentifier($helper.getPropertyName($field, $project)))($field.type $paramName) {
#if ($field.name == $paramName)
    #if (!$field.modifierStatic)
    this.##
    #else
        $classname.##
    #end
#end
#if($field.boolean||$field.primitive||$field.string)
    $field.name = $paramName;
#else
    $field.name = Objects.isNull($paramName)? null : (${field.typeName}) ${paramName}.clone();
#end
}
```
