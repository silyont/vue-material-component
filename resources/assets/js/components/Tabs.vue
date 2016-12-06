<template>
    <div class="tab-panel">
        <div class="tab-nav">
            <ul>
                <li class="tab-item" v-for="tab in tabs" @click="activateTab(tab)" :class="{selected: tab.show}">{{ tab.label }}</li>
            </ul>
            <div class="indicator"></div>
        </div>
        <slot></slot>
    </div>
</template>

<script>
    export default {
        data: function() {
            return {
                tabs: [],
                $_indicator: null,
            };
        },

        mounted: function() {
            this.$_indicator = $(this.$el).find('.indicator');
        },

        methods: {
            registerTab: function(tab) {
                this.tabs.push(tab);
            },

            activateTab: function(tab) {
                // show the tab content
                this.$emit('TabActivationEvent', tab);

                this.moveTabIndicator(tab);
            },

            moveTabIndicator: function(tab) {
                this.$nextTick(function() {
                    // get the tab nav position
                    var $targetTab = $(this.$el).find('.tab-nav .tab-item:eq('+this.tabs.indexOf(tab)+')');
                    // console.log($(this.$el).find('.tab-nav ul .tab-item'));
                    this.$_indicator.css('left', $targetTab.position().left).css('width', $targetTab.width());
                })
                
            }
        }

    }
</script>

<style>
    .tab-nav {
        position: relative;
    }

    ul {
        padding: 0;
        margin: 0;
        list-style: none;
        width: 100%;
    }

    ul > li {
        display: inline-block;
        margin-right: 25px;
        line-height: 36px;
        cursor: pointer;
    }

    .tab-nav .indicator {
        width: 0;
        background-color: #123561;
        height: 2px;
        position: absolute;
        transition: left 0.3s ease, width 0.3s ease;
        left: 0;
    }
</style>