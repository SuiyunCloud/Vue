**Study notes of 《Vue.js 2 Design Patterns and Best Practices》**

# Prerequisites

1. Tools

Node, npm, nvm, Vue Command Line Interface (CLI), vscode, chorme, Vue.js devtools

2. Install vs plugin

   Vue VSCode Extension Pack, it includes Vetur, Vue 2 Snippets, pretteier...

3. Learn to use Emmet to boost develop

# Basic of Vue

1. life cycle
   [Life cycle](life_cycle.png)

2. Parent, child component life cycle
    * beforeCreate() and created() of the parent run first.
    * Then the parent’s template is being rendered, which means the child components get created 
    so now the children’s beforeCreate() and created() hooks execute respecitvely.
    these child components mount to DOM elements, which calls their beforeMount() and mounted() hooks
    ** And only then, after the parent’s template has finished, can the parent be mounted to the DOM, so finally the parent’s beforeMount() and mounted() hooks are called.

3. Computed vs watcher vs methods

    * When to use methods

        To react on some event happening in the DOM

        To call a function when something happens in your component. You can call a methods from computed properties or watchers.

    * When to use computed properties

        You need to compose new data from existing data sources
        You have a variable you use in your template that’s built from one or more data properties
        You want to reduce a complicated, nested property name to a more readable and easy to use one, yet update it when the original property changes
        You need to reference a value from the template. In this case, creating a computed property is the best thing because it’s cached.
        You need to listen to changes of more than one data property

    * When to use watchers

        You want to listen when a data property changes, and perform some action
        You want to listen to a prop value change
        You only need to listen to one specific property (you can’t watch multiple properties at the same time)
        You want to watch a data property until it reaches some specific value and then do something


# Create better UI

1. css animations

```js
// apply animation class
<h1 v-bind:class="{ animated: toggle }">i fade in</h1>


// define animation to fade out
@keyframes fade {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.animated {
  animation: fade 3s;
  opacity: 1;
}
```

2. Using Animate.css
Vue use `transition` package varity animation class and it will apply to the object betwwen label `transition`. And `v-if` used to control when the object fade in and fade out. All available class refer to [https://animate.style/](https://animate.style/)

In order to use the style, css should involved

```html
href="https://cdn.jsdelivr.net/npm/animate.css@3.5.1"
```

There are state as follows:

    v-enter：定义进入过渡的开始状态。在元素被插入之前生效，在元素被插入之后的下一帧移除。

    v-enter-active：定义进入过渡生效时的状态。在整个进入过渡的阶段中应用，在元素被插入之前生效，在过渡/动画完成之后移除。这个类可以被用来定义进入过渡的过程时间，延迟和曲线函数。

    v-enter-to：2.1.8 版及以上定义进入过渡的结束状态。在元素被插入之后下一帧生效 (与此同时 v-enter 被移除)，在过渡/动画完成之后移除。

    v-leave：定义离开过渡的开始状态。在离开过渡被触发时立刻生效，下一帧被移除。

    v-leave-active：定义离开过渡生效时的状态。在整个离开过渡的阶段中应用，在离开过渡被触发时立刻生效，在过渡/动画完成之后移除。这个类可以被用来定义离开过渡的过程时间，延迟和曲线函数。

    v-leave-to：2.1.8 版及以上定义离开过渡的结束状态。在离开过渡被触发之后下一帧生效 (与此同时 v-leave 被删除)，在过渡/动画完成之后移除。

3. render
render used to render HTML in js, work with JSX will be better.

old way

    ```js
    <script type="text/x-template" id="anchored-heading-template">
    <h1 v-if="level === 1">
        <slot></slot>
    </h1>
    <h2 v-else-if="level === 2">
        <slot></slot>
    </h2>
    <h3 v-else-if="level === 3">
        <slot></slot>
    </h3>
    <h4 v-else-if="level === 4">
        <slot></slot>
    </h4>
    <h5 v-else-if="level === 5">
        <slot></slot>
    </h5>
    <h6 v-else-if="level === 6">
        <slot></slot>
    </h6>
    </script>

    Vue.component('anchored-heading', {
    template: '#anchored-heading-template',
    props: {
        level: {
        type: Number,
        required: true
        }
    }
    })
    ```

Compare with reder, code will be shorter

    ```js
    Vue.component('anchored-heading', {
    render: function (createElement) {
        return createElement(
        'h' + this.level,   // 标签名称
        this.$slots.default // 子节点数组
        )
    },
    props: {
        level: {
        type: Number,
        required: true
        }
    }
    })
    ```

