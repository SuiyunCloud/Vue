
## Tools
1. vue-devtools for chorme plugin, easy for debugging
2. vue-cli: set up project basic 

## Component

### Usage
1. Structure of Component
template, script, style

2. import Component
    ```js
    <template>
      <div id="app">
        <img src="./assets/logo.png">
    <!--    3. add compoenet-->
        <HelloWorld/>
      </div>
    </template>

    <script>
      // 1. import component
    import HelloWorld from './components/HelloWorld'

    export default {
      name: 'App',

      // 2. register the component here
      components: {
        HelloWorld
      }
    }
    </script>
    ```

3. global definition
Define a component which can be used globally
```js
Vue.component('connection-status', ConnectionStatus);
```

###  is attribute

  Some label require only specified label can be used, such as only \<tr>, \<td>... can be used in \<table>. In this condition, use is attribute to insert component.

      ```js
      <div id="app">
        <table>
          <tbody is="my-component"></tbody>
        </table>
      </div>
      ```


##  Template syntax
1. {{}} used for control content in label
    ```js
    <template>
      <div>
        <div>{{intro}}</div>
      </div>

    </template>

    <script>
    export default {
      name: 'tmp2',
      data () {
        return {
          intro: 'hello, world2'
        }
      }
    }
    </script>
    ```

2. v-bind: change property of label
    ```js
      <div>{{intro}}</div>

        <h3>Data bind</h3>
        <a href="site">learn Vue</a>
        <a v-bind:href="site">Learn</a>
        <a :href="site">Learn</a>
      </div>
      ```
3. v-on: bind event
      ```js
      <div>
      <h3>Event bind</h3>
        <p><button v-on:click="learn">Learn event</button> </p>
        <p><button @click="learn">Learn event</button> </p>
      </div>

    methods: {
        learn () {
          alert('Congratulations!')
        }
      }
      ```


## Computed properties

Compare to methods, computed result will be cached.

1. basic
```html
<div id="example">
  <p>Original message: "{{ message }}"</p>
  <p>Computed reversed message: "{{ reversedMessage }}"</p>
</div>
```
```js
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // a computed getter
    reversedMessage: function () {
      // `this` points to the vm instance
      return this.message.split('').reverse().join('')
    }
  }
})
```

## Class and Style bindings
1. dynamically toggle class

    the presence of the active class will be determined by the truthiness of the data property isActive
    ```html
    <div v-bind:class="{ active: isActive }"></div>
    <div v-bind:class="classObject"></div>
    ```
    ```js
    data: {
      isActive: true,
      error: null
    },
    computed: {
      classObject: function () {
        return {
          active: this.isActive && !this.error,
          'text-danger': this.error && this.error.type === 'fatal'
        }
      }
    }
    ```

2. toggle style
    ```html
    <div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
    <div v-bind:style="styleObject"></div>
    ```

## Conditional rendering
  1. v-if: remove/insert the element based on the truthiness of the expression value
      ```html
      <h1 v-if="awesome">Vue is awesome!</h1>
      <h1 v-else>Oh no 😢</h1>

      <template v-if="ok">
        <h1>Title</h1>
        <p>Paragraph 1</p>
        <p>Paragraph 2</p>
      </template>

      <div v-if="type === 'A'">
        A
      </div>
      <div v-else-if="type === 'B'">
        B
      </div>
      <div v-else-if="type === 'C'">
        C
      </div>
      <div v-else>
        Not A/B/C
      </div>
      ```

2. v-show: 

doesn’t support the "template" element, nor does it work with v-else. Generally speaking, v-if has higher toggle costs while v-show has higher initial render costs. So prefer v-show if you need to toggle something very often, and prefer v-if if the condition is unlikely to change at runtime.

## List rendering

    ```html
      <ul id="example-1">
        <li v-for="item in items" :key="item.message">
          {{ item.message }}
        </li>
      </ul>
    ```

    ```js
      var example1 = new Vue({
        el: '#example-1',
        data: {
          items: [
            { message: 'Foo' },
            { message: 'Bar' }
          ]
        }
      })
    ```

iterate through the properties of object

      ```html
      <ul id="v-for-object" class="demo">
        <li v-for="value in object">
          {{ value }}
        </li>
      </ul>

      <div v-for="(value, name) in object">
        {{ name }}: {{ value }}
      </div>

      <div v-for="(value, name, index) in object">
        {{ index }}. {{ name }}: {{ value }}
      </div>
      ```
      ```js
      new Vue({
        el: '#v-for-object',
        data: {
          object: {
            title: 'How to do lists in Vue',
            author: 'Jane Doe',
            publishedAt: '2016-04-10'
          }
        }
      })
      ```


## Event handling
1. event modifiers

    .stop
    .prevent
    .capture
    .self
    .once
    .passive
    ```html
    <!-- the click event's propagation will be stopped -->
    <a v-on:click.stop="doThis"></a>

    <!-- the submit event will no longer reload the page -->
    <form v-on:submit.prevent="onSubmit"></form>

    <!-- modifiers can be chained -->
    <a v-on:click.stop.prevent="doThat"></a>

    <!-- just the modifier -->
    <form v-on:submit.prevent></form>

    <!-- use capture mode when adding the event listener -->
    <!-- i.e. an event targeting an inner element is handled here before being handled by that element -->
    <div v-on:click.capture="doThis">...</div>

    <!-- only trigger handler if event.target is the element itself -->
    <!-- i.e. not from a child element -->
    <div v-on:click.self="doThat">...</div>
    ```

2. keyboard code(Deprecated)

    .enter
    .tab
    .delete (captures both “Delete” and “Backspace” keys)
    .esc
    .space
    .up
    .down
    .left
    .right
    ```html
    <input v-on:keyup.enter="submit">  //enter keyboard up will event
    ```


## Form Input binding
1. v-model directive to create two-way data bindings on form input, textarea, and select elements
v-model will ignore the initial value, checked, or selected attributes found on any form elements. It will always treat the Vue instance data as the source of truth. 
    ```html
    <input v-model="message" placeholder="edit me">
    <p>Message is: {{ message }}</p>

    <span>Multiline message is:</span>
    <p style="white-space: pre-line;">{{ message }}</p>
    <br>
    <textarea v-model="message" placeholder="add multiple lines"></textarea>

    <input type="checkbox" id="checkbox" v-model="checked">
    <label for="checkbox">{{ checked }}</label>
    ```

2. modifiers

    .lazy: refresh data after input done not sync

    .number: transfer input as number

    .trim: trim whitespace


## Component

1. pass data to child components with props
    ```js
    // define a component
    Vue.component('blog-post', {
      props: ['title'],
      template: '<h3>{{ title }}</h3>'
    })

    // In parent component to ues it and pass data by 'title' which defined in props
    <blog-post title="My journey with Vue"></blog-post>
    <blog-post title="Blogging with Vue"></blog-post>
    <blog-post title="Why Vue is so fun"></blog-post>
    ```
  
2. listen to child events

  ```js
    // in parent component to listen event 'enlarge-text'
    <blog-post
      ...
      v-on:enlarge-text="postFontSize += 0.1"
    ></blog-post>

    //in child component we use $emit to pass event to parent
    <button v-on:click="$emit('enlarge-text')">
      Enlarge text
    </button>
  ```

3. use slots to distribute content

    Parents can transfer content to child component by replacint label slot

      ```js
      // in child component use slot to define postion which the content should be placed
      Vue.component('alert-box', {
        template: `
          <div class="demo-alert-box">
            <strong>Error!</strong>
            <slot></slot>
          </div>
        `
      })

      //in parent component, content in child component will pass to child 
      <alert-box>
        Something bad happened.   //these content will replace <slot></slot> in child component
      </alert-box>
      ```

4. dynamic components(switch component)

  component can be used.

    ```js
    <component v-bind:is="currentTabComponent"></component>
    ```

5. event bus

  Define a EventBus.js file, 
  ```js
    import Vue from 'vue';
    export default new Vue();
  ```

  Emit event in the event source component with `$emit`
  ```js
  EventBus.$emit('addShoppingItem', this.itemName)
  ```

  Listen to the event in other component with `$on`
  ```js
  EventBus.$on('addShoppingItem', (item) => {
    console.log(`There was an item added! ${item}`);
  })
```