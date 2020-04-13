<template>
  <div @click="btn" class="wrapper">
    请点击我
  </div>
</template>

<script>
export default {
  components: {},
  props: {},
  data() {
    return {
      a: 6,
      name: 'kk'
    };
  },
  methods: {
    btn(){
      console.log(this)
      let obj = {
        name : 'obj',
        A    : function(){
            ()=>{
                console.log(this)
            }
        },
        B    :() => {
          console.log(this)
            // console.log(this.name)
        }
    }
    obj.A(); //输出 obj
    obj.B(); //输出 this
    },
      jicheng() {
      function Parent(name){
        this.name = name;
        this.colors = ["blue","yellow","green"];
      }

      function Child(name,age){
        Parent.call(this,name);
        this.age = age;
      }

      Child.prototype = new Parent();
      Child.prototype.sayAge = function(){
        console.log(this.age);
      }
      let child1 = new Child('kk',22);
      child1.sayAge();
      let p1 = new Parent('zz');
      // p1.__proto__.sayAge();
      console.log('p1',p1);
      console.log('c1',child1);
      console.log('p1p',p1.__proto__);
      console.log('c1c',child1.__proto__)
      console.log('p1',p1)
    },
    // 1、借用构造函数（伪造对象/经典继承）
    one() {
      function Parent(name){
        this.name = name;
      }
      Parent.prototype.sayAge = function(word){
        console.log('99',word);
        let age = 66;
        return age ;
      }
      function Child(){
        Parent.call(this,"parent");
        this.age = 24;
      }
      Child.prototype = new Parent('pp')
      //因为修改了Student原型链,需要把其原型链上构造器重新指向自己
      Child.prototype.constructor = Child;
        let c1 = new Child();
        let p1 = new Parent('kk');
        console.log('p1',p1.sayAge('66'))
        console.log('c1',c1)
        // c1.sayAge();
    },
    two() {
      class Person {
        constructor(age, name) {
            this.age = age;
            this.name = name;
        }
        sayHi(){
            console.log("I'm a Person! age="+this.age+" name="+this.name);
        }
        sayAge() {
          console.log('my age is 22')
        }
      }
      class Student extends Person{
          constructor(sno,age,name) {
              super(age, name);
              this.sno = sno;
          }
      }
      var s = new Student(95001,24,"小红");
      console.log(Student.prototype.constructor);
      s.sayHi();
      s.sayAge();
    }
  },
  created() {
    // this.jicheng()
    // this.one();
    this.two();
  },
  mounted() {}
};
</script>
<style scoped>
.wrapper{}
</style>