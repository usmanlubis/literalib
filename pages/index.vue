<template>
  <main>
    <div class="py-4">
      <div class="container">
        <div class="title border-bottom d-flex align-items-center justify-content-between py-2">
          <h5>Books</h5>
          <div class="d-flex align-items-center ms-auto">
            <div class="dropdown me-2">
              <button class="btn btn-primary dropdown-toggle" type="button" data-bs-toggle="dropdown" aria-expanded="false">
                {{ category }}
              </button>
              <ul class="dropdown-menu">
                <li><button class="dropdown-item" @click="category = 'All Categories'" >All</button></li>
                <li><button class="dropdown-item" @click="category = 'Productivity'" >Productivity</button></li>
                <li><button class="dropdown-item" @click="category = 'Self-help'" >Self-help</button></li>
                <li><button class="dropdown-item" @click="category = 'Fiction'" >Fiction</button></li>
              </ul>
            </div>
            <div class="d-flex align-items-center justify-content-end w-100">
              <span class="me-2">View As</span>
              <button
                class="btn btn-outline-secondary py-1 px-3"
                @click="isGrid = !isGrid">
                {{ isGrid ? 'Grid' : 'List' }}
              </button>
            </div>
          </div>
        </div>
        <div class="list-task row">
          <CardItem
            v-for="(task, index) in filteredBooks"
            :key="index"
            :task="task"
            :is-grid="isGrid"
          />
        </div>
        <div class="action py-2">
          <a v-if="!isCreating" href="#" class="add-button" @click="isCreating = !isCreating">Add Task</a>
          <div v-else class="add-card">
            <div class="card mb-2">
              <div class="card-body d-flex flex-column p-0">
                <input type="text" class="form-control border-0 mb-2" placeholder="Title">
                <textarea class="form-control border-0 small" placeholder="Description" rows="3"></textarea>
              </div>
            </div>
            <div class="button-wrapper d-flex">
              <button class="btn btn-primary me-2">Save</button>
              <button class="btn btn-outline-secondary" @click="isCreating = !isCreating">Cancel</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
  import CardItem from '@/components/Card/CardItem.vue';
  export default {
    name: 'IndexPage',
    components: {
      CardItem
    },
    data() {
      return {
        tasks: [
          {
            title: 'Eat That Frog',
            description: 'Ini Deskripsi',
            isDone: false,
            category: 'Productivity'
          },
          {
            title: 'Meditations',
            description: 'ini deskripsi 2',
            isDone: false,
            category: 'Self-help'
          },
          {
            title: 'Harry Potter',
            description: ' ini deskripsi 3',
            isDone: false,
            category: 'Fiction'
          },
          {
            title: 'The Alchemist',
            description: ' ini deskripsi 4',
            isDone: false,
            category: 'Fiction'
          },
          {
            title: 'Atomic Habits',
            description: ' ini deskripsi 5',
            isDone: false,
            category: 'Self-help'
          }
        ],
        isCreating: false,
        isGrid: false,
        category: 'All Categories',
      }
    },
    computed: {
      filteredBooks() {
        if(this.category === 'All Categories'){
          return this.tasks;
        } else {
          return this.tasks.filter((item) => {
            return item.category === this.category;
            });
        }
      }
    }
  }
</script>
