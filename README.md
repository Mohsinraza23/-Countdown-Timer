# ⏳ Countdown Timer using Streamlit

A simple and interactive countdown timer built using Python and Streamlit. This timer allows users to set a countdown duration, start, stop, and resume the timer while displaying a visually appealing interface. 🚀

## 🎯 Features
- ✅ **Start, Stop, and Resume Countdown**
- ✅ **Beautiful UI with Animations & Hover Effects**
- ✅ **Remembers Remaining Time when Stopped**
- ✅ **Real-Time Countdown Display**
- ✅ **User-Friendly Input and Controls**

---

## 🚀 How It Works
### 1️⃣ Import Required Libraries
```python
import time
import streamlit as st
```
- `time` → Used to create a delay (`time.sleep(1)`) for counting down.
- `streamlit` → Used for creating the web UI.

### 2️⃣ Initialize Session State
```python
if "running" not in st.session_state:
    st.session_state.running = False
if "remaining_time" not in st.session_state:
    st.session_state.remaining_time = 10  # Default time
```
- **Session State** stores variables between reruns.
- `running` → Stores whether the timer is running (`True`) or stopped (`False`).
- `remaining_time` → Stores the remaining countdown time to allow pause and resume.

### 3️⃣ Define Countdown Timer Function
```python
def countdown_timer():
    st.session_state.running = True
    placeholder = st.empty()
    
    while st.session_state.remaining_time >= 0 and st.session_state.running:
        mins, secs = divmod(st.session_state.remaining_time, 60)
        placeholder.markdown(f"""
        <div style='text-align: center; font-size: 40px; font-weight: bold; color: #FF5733;'>
            ⏳ {mins:02}:{secs:02}
        </div>
        """, unsafe_allow_html=True)
        time.sleep(1)
        st.session_state.remaining_time -= 1
    
    if st.session_state.running:
        placeholder.success("🎉 Time's Up! The countdown has finished!")
    else:
        placeholder.warning("⏹ Timer Stopped! Click 'Start' to resume.")
```
- Decreases the time every second if `running` is `True`.
- Stops countdown if `running` is `False` but remembers the remaining time.
- Uses **HTML & CSS** for a beautiful countdown display.

### 4️⃣ Configure Streamlit UI
```python
st.set_page_config(page_title="Countdown Timer", page_icon="⏳", layout="centered")
```
- Sets the page title and icon in the browser.

### 5️⃣ Display Page Heading
```python
st.markdown(
    "<h1 style='text-align: center; color: #4CAF50;'>⏳ Countdown Timer</h1>", 
    unsafe_allow_html=True
)
```
- Creates a **big, bold heading** for the timer using HTML & CSS.

### 6️⃣ User Input for Countdown Time
```python
st.markdown("<p style='font-size:18px; color:#333;'>Enter countdown time in seconds:</p>", unsafe_allow_html=True)

if not st.session_state.running:
    st.session_state.remaining_time = st.number_input(
        "", min_value=1, step=1, value=st.session_state.remaining_time, format="%d",
        key="time_input", help="Set the countdown duration in seconds."
    )
```
- **Allows user input for countdown duration**.
- Input is **disabled** when the timer is running to prevent mid-countdown changes.

### 7️⃣ Add Custom Styling for Buttons
```python
button_style = """
    <style>
        div.stButton > button {
            background-color: #008CBA;
            color: white;
            font-size: 18px;
            padding: 10px 20px;
            border-radius: 8px;
            border: none;
            cursor: pointer;
            transition: 0.3s;
        }
        div.stButton > button:hover {
            background-color: #005f73;
        }
    </style>
"""
st.markdown(button_style, unsafe_allow_html=True)
```
- **Adds stylish blue buttons** with hover effects using CSS.

### 8️⃣ Create Start & Stop Buttons
```python
col1, col2 = st.columns(2)

with col1:
    if st.button("Start Timer 🚀"):
        countdown_timer()

with col2:
    if st.button("Stop Timer ⏹"):
        st.session_state.running = False
```
- **Start Timer 🚀 Button**: Starts the countdown.
- **Stop Timer ⏹ Button**: Stops the timer but remembers the remaining time.

---

## 🎯 Step-by-Step Execution
1️⃣ **User enters countdown time** (e.g., 10 seconds).
2️⃣ **Clicks "Start Timer 🚀"** → Timer starts counting down.
3️⃣ **Clicks "Stop Timer ⏹"** → Timer pauses at the current time.
4️⃣ **Clicks "Start Timer 🚀" again** → Timer resumes from the same spot.
5️⃣ **When time reaches 0** → Shows **"🎉 Time's Up!"**

## 🔧 Installation & Usage
### 1️⃣ Install Dependencies
```sh
pip install streamlit
```
### 2️⃣ Run the Streamlit App
```sh
streamlit run app.py
```
---

## 💡 Summary
✅ **Starts from where it was paused instead of resetting.**
✅ **Remembers the remaining time when stopped.**
✅ **Beautiful UI with animations & hover effects.**
✅ **Simple and easy to use!**

🚀 Let me know if you have any questions or want to improve the project! 🔥

