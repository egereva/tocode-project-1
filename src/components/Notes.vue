<template>
    <!-- note list -->
    <div class="notes">
        <div class="note" :class="[{full: !grid, important: note.priority === 'important', veryImportant: note.priority === 'veryImportant' }]" v-for="(note, index) in notes" :key="index">
            <div class="note-header" :class="{full: !grid}">
                <input v-if="notes[index].selected" type="text">
                <p @click="editTitle(index)">{{ note.title }}</p>
                <p style="cursor: pointer;" @click="removeNote(index)">x</p>
            </div>
            <div class="note-body">
                <p>{{ note.descr }}</p>
                <span>{{ note.date }}</span>
            </div>
        </div>
    </div>
</template>

<script>
    export default  {
        props: {
            notes: {
                type: Array,
                required: true
            },
            grid: {
                type: Boolean,
                required: true
            },

        },
        data () {
          return {

          }
        },
        methods: {
            removeNote(index) {
                console.log(`Note id - ${index} removed`)
                this.$emit('remove', index)
            },
            editTitle(index) {
                this.notes[index].selected = true

            }

        },

    }
</script>

<style lang="scss">
    .notes {
        display: flex;
        align-items: center;
        justify-content: space-between;
        flex-wrap: wrap;
        padding: 40px 0;
    }

    .note {
        width: 48%;
        padding: 18px 20px;
        margin-bottom: 20px;
        background: #fff;
        transition: all .25s cubic-bezier(.02,.01,.47,1);
        box-shadow: 0 30px 30px rgba(0,0,0,0.2);
        &:hover {
            box-shadow: 0 30px 30px rgba(0,0,0,0.4);
            transform: translate(0, -6px);
            transition-delay: 0s !important;
        }
        &.full {
            width: 100%;
            text-align: center;
        }
        &.important {
            outline: 2px solid #ffe12d;
        }
        &.veryImportant {
            outline: 2px solid red;
        }
    }

    .note-header {
        display: flex;
        align-items: center;
        justify-content: space-between;

        h1 {
            font-size: 32px;
        }

        p {
            color: #402caf;
            font-size: 22px;
        }
        svg {
            margin-right: 12px;
            color: #999999;
            &.active {
                color: #402caf;
            }
            &:last-child {
                margin-right: 0;
            }
        }
        &.full {
            justify-content: center;
            p {
                margin-right: 16px;
                &:last-child {
                    margin-right: 0;
                }
            }
        }
    }

    .note-body {
        p {
            margin: 20px 0;
        }

        span {
            font-size: 14px;
            color: #999999;
        }
    }

</style>
