# Time--Calculator
test free  code camp

def add_time(start, duration, day=None):
    # Extract the hours and minutes from the start time
    start_time, period = start.split()
    start_hour, start_minute = map(int, start_time.split(':'))

    # Extract the hours and minutes from the duration time
    duration_hour, duration_minute = map(int, duration.split(':'))

    # Calculate the total minutes
    total_minutes = start_hour * 60 + start_minute + duration_hour * 60 + duration_minute

    # Calculate the new time and period
    new_minutes = total_minutes % 60
    new_hour = (total_minutes // 60) % 12
    new_period = period

    # Calculate the number of days passed
    days_passed = total_minutes // 60 // 12

    # Determine the new period and adjust the new hour accordingly
    if period == 'AM':
        if new_hour == 0:
            new_hour = 12
        if days_passed % 2 == 1:
            new_period = 'PM'
    else:
        if new_hour == 0:
            new_hour = 12
        if days_passed % 2 == 0:
            new_period = 'AM'

    # Determine the new day of the week
    if day:
        day = day.lower()
        days_of_week = ['monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday', 'sunday']
        day_index = days_of_week.index(day)
        new_day_index = (day_index + days_passed) % 7
        new_day = days_of_week[new_day_index].capitalize()
        new_time = f"{new_hour}:{str(new_minutes).zfill(2)} {new_period}, {new_day}"
    else:
        new_time = f"{new_hour}:{str(new_minutes).zfill(2)} {new_period}"

    if days_passed == 1:
        new_time += " (next day)"
    elif days_passed > 1:
        new_time += f" ({days_passed} days later)"

    return new_time
