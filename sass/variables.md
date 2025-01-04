### 变量的定义

变量使用$开头，变量还可以引用其他的变量，编译后会进行替换

```scss
$base-color: #c6538c;
$border-dark: rgba($base-color, 0.88);
.alert {
  border: 1px solid $border-dark;
}
```

### 变量的默认值

变量的默认值使用!default来表示，若外部没定义则使用默认值，外部定义了则使用外部的值。一般用于用户可以自定义主题

```scss
$black: #000 !default;
$border-radius: 0.25rem !default;
$box-shadow: 0 0.5rem 1rem rgba($black, 0.15) !default
```

### 变量的作用域

变量的作用域分为局部作用域与全局作用域，与JavaScript一致
在局部作用域中可以使用!global来提升至全局作用域

```scss
$global-variable: orange; 
.content {
  $local-variable: skyblue;
  color: $local-variable;
}
.sidebar {
  color: $global-variable;
  // This would fail, because $local-variable isn't in scope:
  background-color:  $local-variable;
}
```

### 控制流范围重新赋值

```scss
@use "sass:color";
$dark-theme: true !default;
$primary-color: #f8bbd0 !default;
$accent-color: #6a1b9a !default;

@if $dark-theme {
  $primary-color: color.scale($primary-color, $lightness:60%);
  $accent-color: color.scale($accent-color, $lightness:60%);
}

.button {
  background-color: $primary-color;
  border: 1px solid $accent-color;
  border-radius: 3px;
}
```


### 高级函数获取变量

```scss
@use "sass:map";

$theme-colors: (
  "success": #28a745,
  "info": #17a2b8,
  "warning": #ffc107,
);

.alert {
  // Instead of $theme-color-#{warning}
  background-color: map.get($theme-colors, "warning");
}
```