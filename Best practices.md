**Study notes of 《Vue.js 2 Design Patterns and Best Practices》**

# Prerequisites

1. Tools

Node, npm, nvm, Vue Command Line Interface (CLI), vscode, chorme, Vue.js devtools

2. Install vs plugin
   Vue VSCode Extension Pack, it includes Vetur, Vue 2 Snippets, pretteier...

3. Learn to use Emmet to boost develop

# Basic of Vue

1. life cycle
   [](life_cycle.png)

2. Parent, child component cycle
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

# Vuex
