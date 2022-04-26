<template>
<div>
  <h1>{{rm}}m {{rs}}s left</h1>
  </div>
</template>

<style>
  h1 {
    color: white;
    text-align: center;
    font-size: 150px;
  }
</style>
<script lang="ts">


  // Create a schedule interface
  interface schedule {
    start_hour: number,
    start_minute: number,
    end_hour: number,
    end_minute: number,
  }

  // Create an array of schedules
  var schedules = [
    {
      start_hour: 7,
      start_minute: 15,
      end_hour: 8,
      end_minute: 0,
    },
    {
      start_hour: 8,
      start_minute: 5,
      end_hour: 8,
      end_minute: 50,
    },
    {
      start_hour: 8,
      start_minute: 55,
      end_hour: 9,
      end_minute: 40,
    },
    {
      start_hour: 10,
      start_minute: 0,
      end_hour: 10,
      end_minute: 45,
    },
    {
      start_hour: 10,
      start_minute: 50,
      end_hour: 11,
      end_minute: 35,
    },
    {
      start_hour: 12,
      start_minute: 45,
      end_hour: 13,
      end_minute: 30,
    },
    {
      start_hour: 13,
      start_minute: 35,
      end_hour: 14,
      end_minute: 20,
    },
    {
      start_hour: 14,
      start_minute: 25,
      end_hour: 15,
      end_minute: 10,
    },
    {
      statrt_hour: 15,
      start_minute: 15,
      end_hour: 16,
      end_minute: 0,
    }
  ]

  // Get the current hour and minute
  var current_hour = new Date().getHours()
  var current_minute = new Date().getMinutes()

  // Get current or next schedule
  function getNextSchedule() {
    for (var i = 0; i < schedules.length; i++) {
      var schedule = schedules[i]
      if (current_hour < schedule.end_hour) {
        return schedule
      } else if (current_hour == schedule.end_hour) {
        if (current_minute < schedule.end_minute) {
          return schedule
        }
      }
    }
    return schedules[0]
  }
  let current_schedule = getNextSchedule();


  // Create two time objects and calculate the difference
  // Current time
  var current = new Date()
  // Create second object with the next schedule
  var next = new Date()
  next.setHours(current_schedule.end_hour-1)
  next.setMinutes(current_schedule.end_minute)
  next.setSeconds(0)

  // Calculate the difference
  var diff = new Date(next.getTime() - current.getTime())

  export default ({

    asyncData() {
      return {  h:diff, m:current_minute, c:diff, rh:diff.getHours(), rm:diff.getMinutes(),  rs:diff.getSeconds() }
    },
    head() {
    return {
      //Refresh meta
      meta: [
        {
          charset: 'utf-8'
        },
        {
          name: 'viewport',
          content: 'width=device-width, initial-scale=1'
        },
        {
         "http-equiv": 'refresh',
          content: '1'
        }
      ],
    }
  }
  })


</script>
