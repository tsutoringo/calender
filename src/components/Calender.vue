<script lang="ts" setup>
const props = withDefaults(
  defineProps<{
    today?: Date;
    viewing?: Date;
    mini?: boolean;
  }>(),
  {
    today: () => new Date(),
    viewing: () => new Date(),
    mini: false
  }
);

const firstDay = new Date(props.viewing.getFullYear(), props.viewing.getMonth(), 1);
const lastDay = new Date(props.viewing.getFullYear(), props.viewing.getMonth() + 1, 0);

const thisWeek = Math.ceil((props.viewing.getDate() + firstDay.getDay()) / 7);

const weekOfDays = [ 'Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat' ];
const miniWeekOfDays = [ 'S', 'M', 'T', 'W', 'T', 'F', 'S' ];

const getWeek = (weekPos: number) => 
  new Array(7).fill(0).map((_, day) =>
    new Date(
      firstDay.getFullYear(),
      firstDay.getMonth(),
      (weekPos * 7 + day + 1) - firstDay.getDay()
    )
  );
</script>

<template>
  <div class="calender" :class="{
    'mini-calender': mini
  }">
    <header>
      <div class="title">
        <h1> {{ viewing.getMonth() + 1 }} </h1>
        <h2 v-if="!mini"> {{ viewing.getFullYear() }} </h2>
      </div>
      <div class="mini-calenders" v-if="!mini">
        <Calender :viewing="new Date(viewing.getFullYear(), viewing.getMonth() - 1, 1)" mini :today="props.today"/>
        <Calender :viewing="new Date(viewing.getFullYear(), viewing.getMonth() + 1, 1)" mini :today="props.today"/>
      </div>
    </header>
    <table>
      <thead>
        <tr v-if="!mini">
          <th> <span>{{ weekOfDays[0] }}</span> </th><th> {{ weekOfDays[1] }} </th><th> {{ weekOfDays[2] }} </th><th> {{ weekOfDays[3] }} </th><th> {{ weekOfDays[4] }} </th><th> {{ weekOfDays[5] }} </th><th> {{ weekOfDays[6] }} </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="week in 6" class="week" :class="[`week-${week}`, viewing.getFullYear() == today.getFullYear() && viewing.getMonth() == today.getMonth() && thisWeek == week ? 'this-week':'']">
          <td v-for="date in getWeek(week - 1)" class="date" :class="[
            date.getMonth() < viewing.getMonth() ?
              'last-month' :
            date.getMonth() > viewing.getMonth() ?
              'next-month' :
              'this-month',
            date.getDate() == today.getDate() && date.getMonth() == today.getMonth() ? 'today' : '',
            [
              'sunday',
              'monday',
              'tuesday',
              'wednesday',
              'thursday',
              'friday',
              'saturday'
            ][date.getDay()]
          ]">
            <span> {{ date.getDate() }} </span>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style lang="scss" scoped>
.calender {
  font-size: 16px;
  padding: 2em;
  color: #223E53;
  
  > header {
    display: flex;
    padding-bottom: 1em;

    > .title {
      flex: 1;
      display: flex;
      align-items: baseline;

      h1, h2 {
        margin: 0;
        display: inline-block;
        padding: 0 2px;
      }

      h1 {
        font-size: 6em;
        font-weight: bold;
      }
    }

    > .mini-calenders {
      display: flex;
    }
  }

  table {
    font-size: 1.5em;
    font-weight: bold;
    table-layout: fixed;
    border-collapse: collapse;
    --border-color: 10px;

    th, td {
      width: 3.2em;
    }

    th {
      text-align: left;
      font-size: 0.5em;
      padding: 2px;
      padding-left: 5px;
      border: 0.5px solid #223E53;
    }

    td.date.last-month, td.date.next-month {
      opacity: 0.4;
    }

    td.sunday {
      color: #E40051;
    }

    td.saturday {
      color: #0049ae;
    }

    td.date {
      height: 3.2em;
      vertical-align: top;
      padding-left: 5px;
      box-sizing: border-box;
    }

    td {
      border: 0.5px solid #223E53;
    }

    :is(th, td):first-child { border-left: none }
    :is(th, td):last-child { border-right: none }
    tr:last-child > td { border-bottom: none }
  }

  &.mini-calender {
    flex: 1;
    font-size: 0.2em;

    table {
      text-align: center;

      td.date {
        padding: 0 2px;
      }

      td, th {
        border: none;
      }
    }
  }
}
</style>