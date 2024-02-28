# Code examples

## Array iterator
```
fn loop;

  call array::get "array" count;
  println "$count^ = $ret^";

  var count + 1;
  call array::size "array";
  if count < ret
    call loop;
  end
nf;

fn main;
  var count = 0;
  call array::new "array";
  call array::append "array" 4;
  call array::append "array" 2;
  call array::append "array" 6;
  call array::append "array" 9;
  call loop;
  return 0;
nf;
```
Alternative (from 2.1)
```
fn main;
  var count = 0;
  call array::new "array";
  call array::append "array" 4;
  call array::append "array" 2;
  call array::append "array" 6;
  call array::append "array" 9;
  
  loop;

    call array::get "array" count;
    println "$count^ = $ret^";

    var count + 1;
    call array::size "array";
    if count < ret
    else
    break;
    end
  
  lend;
  return 0;
nf;
```

## Calculator
```
fn main;

  print "Enter 1st num: ";
  scanln num1;
  cast num1 float;

  print "Enter operator: ";
  scanln op;

  print "Enter 2st num: ";
  scanln num2;
  cast num2 float;

  var result = 0;

  if op == "+"
    cp result num1;
    var result + num2;
  end
  if op == "-"
    cp result num1;
    var result - num2;
  end
  if op == "*"
    cp result num1;
    var result * num2;
  end
  if op == "/"
    cp result num1;
    var result / num2;
  end

  println "Result: $result^";

  return 0;
nf;
```

## ImGui Menu (2.0 Pre-release only)
```
fn apploop;

  call ImGui::get_callback_clicked "button1";
  if ret == 1
    call ImGui::delete_item "checkbox1";
    println "Button 1 Clicked";
    call ImGui::set_callback_clicked "button1" 0;
  end

  call ImGui::get_value "checkbox1";
  if ret == 1
    call ImGui::set_value "checkbox1" 0 "bool";
    println "Checkbox value changed";
  end


  call ImGui::is_imgui_running;
  if ret == 1
    call apploop;
  end
nf;

fn main;
  call ImGui::create_imgui_thread "Watermelon with imgui" "Watermelon with imgui is cool" 800 600;

  call ImGui::add_text "It's cool isn't it?" "txt";

  call ImGui::add_button "Delete checkbox" "button1";
  call ImGui::add_checkbox "Test checkbox" "checkbox1";

  call apploop;

  return 0;
nf;
```
Alternative (from 2.1)
```
fn main;
  call ImGui::create_imgui_thread "Watermelon with imgui" "Watermelon with imgui is cool" 800 600;

  call ImGui::add_text "It's cool isn't it?" "txt";

  call ImGui::add_button "Delete checkbox" "button1";
  call ImGui::add_checkbox "Test checkbox" "checkbox1";

  loop;
    call ImGui::get_callback_clicked "button1";
    if ret == 1
      call ImGui::delete_item "checkbox1";
      println "Button 1 Clicked";
      call ImGui::set_callback_clicked "button1" 0;
    end

    call ImGui::get_value "checkbox1";
    if ret == 1
      call ImGui::set_value "checkbox1" 0 "bool";
      println "Checkbox value changed";
    end


    call ImGui::is_imgui_running;
    if ret == 1
    else
      break;
    end
  lend;

  return 0;
nf;
```

## Scopes
```
fn main;
  call scope::new_scope "test";
  call scope::change_scope "test";
  var a = 123;
  call scope::change_scope "global";
  println "a is: $a^"; ? will not print anything because a is defined in test -?
  call scope::change_scope "test";
  println "a is: $a^"; ? will print because we changed to test -?
  call scope::delete_scope "test";
  return 0;
nf;
```

## Timed var
```
fn main;
  var a = 123;
  call timedvar::seconds "a" 2;
  println "a is: $a^"; ? will print because it is not timed out yet -?
  sleep 3;
  println "a is: $a^"; ? will not print because a is timed out -?
  return 0;
nf;
```
