<template>
  <q-page>
    <q-input
      outlined
      bottom-slots
      v-model="newMission"
      label="Add new task"
      counter
      @keyup.enter="addTask"
    >
      <template v-slot:append>
        <q-icon clickable name="add" @click="addTask" class="cursor-pointer" />
      </template>
    </q-input>
    <q-list bordered separator>
      <q-item
        v-for="(task, index) in tasks"
        :key="task.id"
        :class="!task.finished ? 'bg-yellow-5' : 'bg-green-5 '"
      >
        <q-item-section side top>
          <q-checkbox v-model="task.finished" @click="orderTasks" />
        </q-item-section>

        <q-item-section>
          <q-item-label :class="{ 'text-strike': task.finished }">
            {{ task.mission }}</q-item-label
          >
        </q-item-section>
        <q-btn
          round
          color="red"
          size="md"
          icon="remove"
          @click="removeTask(index)"
        />
        <q-btn
          round
          color="green"
          size="md"
          icon="edit"
          @click="
            prompt = true;
            indexd = index;
          "
        />
      </q-item>
    </q-list>

    <q-dialog v-model="prompt" persistent>
      <q-card style="min-width: 350px">
        <q-card-section>
          <div class="text-h6">Edit Task</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <q-input
            dense
            v-model="input"
            autofocus
            @keyup.enter="
              editTask(indexd);
              prompt = false;
              input = '';
            "
            @keyup.esc="
              prompt = false;
              input = '';
            "
          />
        </q-card-section>

        <q-card-actions align="right" class="text-primary">
          <q-btn flat label="Cancel" v-close-popup @click="input = ''" />
          <q-btn
            flat
            label="Edit Task"
            v-close-popup
            @click="editTask(indexd)"
          />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </q-page>
</template>


<script>
export default {
  data() {
    return {
      newMission: "",
      tasks: [
        {
          id: 1,
          mission: "Zrob w koncu tą apke co?",
          finished: false,
        },
        {
          id: 2,
          mission: "Zrob w koncu tą apke co? Prosze",
          finished: false,
        },
        {
          id: 3,
          mission: "Zrob w koncu tą apke co? No kurwa",
          finished: true,
        },
      ],
      prompt: false,
      input: "",
      indexd: 0,
    };
  },
  methods: {
    addTask() {
      if (this.newMission.length > 0) {
        this.tasks.push({
          mission: this.newMission,
          finished: false,
        });
      } else {
        return;
      }
      this.newMission = "";
      this.orderTasks();
      console.log("addTask");
    },
    orderTasks() {
      this.tasks.sort((a, b) => (a.finished >= b.finished ? 1 : -1));
      console.log("orderTask");
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
      console.log("removeTask");
    },
    editTask(indexd) {
      this.tasks[indexd].mission = this.input;
    },
  },
};
</script>
