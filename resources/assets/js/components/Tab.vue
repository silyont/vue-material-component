<template>
    <div class="tab-pane" v-show="show">
        <slot></slot>
    </div>
</template>

<script>
    export default {
        props: [
            'label', 'selected'
        ],

        data: function() {
            return {
                show: false,
                width: null,
            }
        },

        created: function() {
            var self = this;

            // call parent to register this tab
            this.$parent.registerTab(this);

            // display the tab content if the tab is selected by default
            if (typeof this.selected != 'undefined' && this.selected !== null) {
                this.show = true;
                this.$parent.moveTabIndicator(this);
            }

            // handle tab click event
            this.$parent.$on('TabActivationEvent', function(tab) {
                self.show = (self === tab);
            });
        }
    }
</script>