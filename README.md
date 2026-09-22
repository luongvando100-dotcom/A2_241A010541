# BÁO CÁO THỰC HÀNH: LAB A2
**Môn học:** Lập trình trên các thiết bị di động (INT4211)  
**Đề tài:** Xử lý sự kiện vòng đời (Activity Lifecycle), Lưu trạng thái (Instance State) & Quản lý phiên bản Git/GitHub  

---

## 📌 1. Thông Tin Chung

| Mục | Chi tiết |
| :--- | :--- |
| **Họ và tên sinh viên** | Lương Văn Đô |
| **Mã số sinh viên (MSSV)** | 241A010541 |
| **Lớp học phần** | 26INT421104 |
| **Thiết bị thử nghiệm** | Google Pixel 8 / Pixel 10 Pro (Emulator) |
| **Môi trường & Hệ điều hành** | Android API 37.2 |
| **Repository URL** | [StopwatchApp Repository](https://github.com/ten-cua-ban/StopwatchApp)  |

---

## 🧪 2. Bảng Kiểm Thử Thực Nghiệm (5 Kịch Bản Bắt Buộc)

| STT | Kịch bản / Thao tác thử nghiệm | Kết quả kỳ vọng (Expected) | Quan sát thực tế | Đánh giá |
| :---: | :--- | :--- | :--- | :---: |
| **01** | Xoay màn hình khi đồng hồ đang chạy | Đồng hồ chạy tiếp tục, không bị reset về 0; số lần tạo lại (`recreateCount`) tăng thêm 1 | Thời gian chạy liên tục, nhãn hiển thị số lần tạo lại tăng 1 | :white_check_mark: Đạt |
| **02** | Nhấn phím Home, chờ ~10s, mở lại app | Thời gian hiển thị được cộng bù chính xác ~10 giây đã trôi qua | Bộ đếm cập nhật bù đủ thời gian ngầm | :white_check_mark: Đạt |
| **03** | Bấm Tạm dừng rồi tiến hành xoay màn hình | Đồng hồ giữ nguyên trạng thái tạm dừng và giữ đúng con số hiện tại | Giữ nguyên thời gian tại điểm dừng, không chạy tiếp | :white_check_mark: Đạt |
| **04** | Bật "Không giữ hoạt động" (*Don't keep activities*), nhấn Home rồi mở lại | Activity bị hệ thống hủy hoàn toàn và tạo mới lại; dữ liệu thời gian vẫn chính xác | Khôi phục đúng từ `savedInstanceState` | :white_check_mark: Đạt |
| **05** | Nhấn Back để thoát hẳn ứng dụng, sau đó mở lại app | Ứng dụng khởi động mới hoàn toàn, thời gian đặt lại về 00:00.0 | Đặt lại ban đầu, biến đếm tạo lại về 0 | :white_check_mark: Đạt |

---

## 📸 3. Minh Họa Kết Quả Kiểm Thử

> *Lưu ý: Đặt các file ảnh vào thư mục `./screenshots/` trong repo hoặc thay thế bằng đường dẫn ảnh tương ứng.*

### Kịch bản 1 & 2: Xoay màn hình và chạy ngầm qua Home

| Kịch bản 1 (Xoay ngang khi đang chạy) | Kịch bản 2 (Sau khi nhấn Home ~10s) |
| :---: | :---: |
| ![Kịch bản 1]<img width="637" height="689" alt="Hình ảnh1" src="https://github.com/user-attachments/assets/3f6e74aa-f980-412b-b899-80537d1ea1cf" /> | ![Kịch bản 2]<img width="639" height="749" alt="Hình ảnh2" src="https://github.com/user-attachments/assets/7875c3dc-7e90-4889-baa8-96bbeb64e703" /> |

### Kịch bản 3: Tạm dừng và Xoay màn hình

| Trước khi xoay màn hình | Sau khi xoay màn hình |
| :---: | :---: |
| ![Kịch bản 3 Trước]<img width="563" height="626" alt="Hình ảnh3" src="https://github.com/user-attachments/assets/e712ec6f-bcb6-4ed0-b74a-4e800b08bd4c" /> | ![Kịch bản 3 Sau]<img width="620" height="652" alt="Hình ảnh3 1" src="https://github.com/user-attachments/assets/22b26db9-2758-45da-8650-0ff07e7d0faf" /> |

### Kịch bản 4 & 5: Kiểm tra hủy Activity & Thoát hoàn toàn

| Kịch bản 4 (Don't keep activities) | Kịch bản 5 (Nhấn Back thoát hoàn toàn) |
| :---: | :---: |
| ![Kịch bản 4]<img width="624" height="668" alt="Hình ảnh4" src="https://github.com/user-attachments/assets/96b7468d-2d2a-4b2a-b977-425191df6f95" /> | ![Kịch bản 5]<img width="579" height="673" alt="Hình ảnh5" src="https://github.com/user-attachments/assets/1e2539dd-f437-47b1-a662-49807b21463c" /> |

---

## 📋 4. Nhật Ký Hệ Thống (Logcat Lifecycle)

**Quy trình thực nghiệm kịch bản:**
1. Khởi động ứng dụng, bấm **Start**.
2. Chờ ứng dụng đếm thời gian trong vài giây.
3. Thực hiện xoay màn hình thiết bị.
4. Ghi nhận chuỗi vòng đời qua TAG `A2_241A010541_Lifecycle`: `onPause()` $\rightarrow$ `onSaveInstanceState()` $\rightarrow$ `onDestroy()` $\rightarrow$ `onCreate()` $\rightarrow$ `onStart()` $\rightarrow$ `onResume()`.

![Logcat Lifecycle]<img width="1652" height="252" alt="Hình ảnh6" src="https://github.com/user-attachments/assets/2f734b43-812e-4629-aa8f-faeffd9b1b2d" />

---

## 🐙 5. Quản Lý Phiên Bản Git & GitHub

- **Đường dẫn Repository:** `https://github.com/ten-cua-ban/StopwatchApp`
- **Nhánh thực hiện:** `master`
- **Lịch sử Git commit:** Đảm bảo tối thiểu 3 commit rõ ràng theo tiến độ hoàn thành.

![Git Log History]<img width="1619" height="377" alt="Hình ảnh7" src="https://github.com/user-attachments/assets/55c51c01-e73b-40e0-aa81-0685875eda35" />

---

## 💡 6. Trả Lời Câu Hỏi Phân Tích

#### Câu 1: Vai trò của phương thức `onSaveInstanceState()` là gì?
> **Trả lời:** `onSaveInstanceState()` dùng để lưu trữ dữ liệu tạm thời (UI state, biến đếm thời gian, danh sách mốc thời gian...) vào đối tượng `Bundle` trước khi Activity bị hệ thống hủy bỏ do các thay đổi cấu hình (như xoay màn hình) hoặc thiếu hụt tài nguyên. Khi Activity được khởi tạo lại, dữ liệu này sẽ được khôi phục tại `onCreate(Bundle savedInstanceState)` hoặc `onRestoreInstanceState(Bundle savedInstanceState)`, giúp duy trì trải nghiệm liền mạch cho người dùng.

#### Câu 2: Tại sao phải gọi `removeCallbacks()` trong Handler?
> **Trả lời:** Khi sử dụng `Handler` để tạo vòng lặp cập nhật giao diện thông qua `Runnable`, việc gọi `handler.removeCallbacks(ticker)` khi tạm dừng hoặc hủy Activity (`onPause()`, `onDestroy()`) là bắt buộc để hủy các tác vụ đang xếp hàng. Nếu không gỡ bỏ, `Runnable` vẫn tiếp tục chạy ngầm và giữ tham chiếu tới Activity đã bị hủy, dẫn đến hiện tượng rò rỉ bộ nhớ (**Memory Leak**) và lỗi ứng dụng.

#### Câu 3: Sự khác nhau giữa `onPause()` và `onDestroy()`?
> **Trả lời:**
> - `onPause()`: Được gọi khi Activity mất quyền tương tác trực tiếp với người dùng (ví dụ: bị che một phần bởi Dialog, màn hình khóa hoặc người dùng bấm phím Home). Activity vẫn tồn tại trong bộ nhớ và lưu trữ đầy đủ trạng thái.
> - `onDestroy()`: Được gọi khi Activity bị giải phóng hoàn toàn khỏi bộ nhớ, hoặc do người dùng thoát hẳn ứng dụng (bấm Back), gọi lệnh `finish()`, hoặc do hệ thống Android tiến hành cấu hình lại môi trường (xoay ngang/dọc thiết bị).

#### Câu 4: Vì sao ứng dụng cần xử lý sự kiện xoay màn hình?
> **Trả lời:** Mặc định trong Android, thao tác xoay hướng màn hình là một sự kiện thay đổi cấu hình (*Configuration Change*). Hệ thống sẽ tự động hủy Activity hiện tại (`onDestroy`) và tạo mới lại hoàn toàn một thể hiện khác (`onCreate`). Nếu không bắt sự kiện và lưu dữ liệu thông qua cơ chế `onSaveInstanceState()`, toàn bộ các biến đếm và trạng thái của đồng hồ sẽ bị khôi phục về trạng thái khởi tạo mặc định ban đầu.

---

## ⭐ 7. Tính Năng Nâng Cao Đã Triển Khai

| Mã tính năng | Tên tính năng | Mô tả chức năng & Kỹ thuật xử lý | Trạng thái |
| :---: | :--- | :--- | :---: |
| **NC1** | **Nút Vòng (Lap)** | Lưu mốc thời gian hiện tại vào `ArrayList<String>`, hiển thị cuộn qua `ScrollView`. Dữ liệu các vòng được lưu giữ đầy đủ qua `KEY_LAP_LIST` khi xoay màn hình. | :white_check_mark: Hoàn thành |
| **NC2** | **Dừng khi ra nền** | Thêm `CheckBox "Dừng khi ra nền"`. Tại vòng đời `onStop()`, nếu ô kiểm được tick chọn, hệ thống sẽ tự động gọi `pauseStopwatch()` và giữ trạng thái tick qua Bundle. | :white_check_mark: Hoàn thành |
| **Bonus** | **Rung phản hồi (Haptic Feedback)** | Tích hợp quyền `VIBRATE`, kích hoạt rung nhẹ thiết bị (150ms) bằng `Vibrator` khi người dùng nhấn nút Đặt lại (Reset). | :white_check_mark: Hoàn thành |
| **Bonus** | **Cảnh báo vượt mốc** | Đổi màu số hiển thị của `TextView` từ màu mặc định sang màu Đỏ (`Color.RED`) khi bộ đếm vượt qua mốc 60 giây (1 phút). | :white_check_mark: Hoàn thành |

### Minh họa tính năng nâng cao

#### NC1: Nút Vòng (Lap) — Màn hình dọc & Khi xoay ngang
| Màn hình dọc (Danh sách vòng) | Khi xoay màn hình ngang (Không mất danh sách) |
| :---: | :---: |
| <img src="DÁN_LINK_ẢNH_NC1_DỌC_VÀO_ĐÂY<img width="407" height="553" alt="Hình ảnh8" src="https://github.com/user-attachments/assets/a133af1b-dc45-4e75-b3db-cd616d3ddc68" />/> | <img src="DÁN_LINK_ẢNH_NC1_NGANG_VÀO_ĐÂY<img width="540" height="263" alt="Hình ảnh9" src="https://github.com/user-attachments/assets/f09fbf2f-34b8-4830-b353-3d90eaee3843" />/> |

#### NC2: CheckBox "Dừng khi ra nền"
| CheckBox kích hoạt khi chạy |
| :---: |
| <img src="DÁN_LINK_ẢNH_NC2_VÀO_ĐÂY<img width="393" height="676" alt="Hình ảnh10" src="https://github.com/user-attachments/assets/47fd25b3-538d-4450-9531-21a56df5bd1f" />/> |

---

## 💻 8. Mã Nguồn Cốt Lõi
### 1. Dán vào `AndroidManifest.xml`

```xml
<uses-permission android:name="android.permission.VIBRATE" />
```
### 2. Dán vào `activity_main.xml` (Phần Giao diện)

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center_horizontal"
    android:orientation="vertical"
    android:padding="16dp">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/title"
        android:textSize="20sp"
        android:textStyle="bold" />

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="4dp"
        android:text="@string/student" />

    <TextView
        android:id="@+id/tvTime"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="32dp"
        android:fontFamily="monospace"
        android:text="@string/zero_time"
        android:textSize="56sp"
        android:textStyle="bold" />

    <TextView
        android:id="@+id/tvStatus"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="8dp"
        android:text="@string/status_paused"
        android:textSize="16sp" />

    <CheckBox
        android:id="@+id/cbStopOnBackground"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:text="Dừng khi ra nền" />

    <!-- Cụm 3 nút bấm (Start - Lap - Reset) -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="24dp"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btnStartPause"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="@string/start" />

        <Button
            android:id="@+id/btnLap"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_marginStart="8dp"
            android:layout_weight="1"
            android:text="Vòng" />

        <Button
            android:id="@+id/btnReset"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_marginStart="8dp"
            android:layout_weight="1"
            android:text="@string/reset" />
    </LinearLayout>

    <TextView
        android:id="@+id/tvRecreate"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:textSize="14sp" />

    <!-- Khu vực cuộn hiển thị danh sách Vòng -->
    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_marginTop="16dp"
        android:layout_weight="1">

        <TextView
            android:id="@+id/tvLapList"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="center_horizontal"
            android:textSize="16sp" />
    </ScrollView>
</LinearLayout>



## 3. Dán vào MainActivity.java (Phần Code gộp)

```xml
<uses-permission android:name="android.permission.VIBRATE" />
package vn.edu.vhu.ltdd.a2stopwatch;

import android.content.Context;
import android.graphics.Color;
import android.os.Build;
import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.SystemClock;
import android.os.VibrationEffect;
import android.os.Vibrator;
import android.util.Log;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.TextView;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

import java.util.ArrayList;
import java.util.Locale;

public class MainActivity extends AppCompatActivity {
    // Lab A2 - Quan ly vong doi va luu trang thai Activity
    private static final String TAG = "A2_241A010541_Lifecycle";

    // Khóa lưu trạng thái vào Bundle
    private static final String KEY_RUNNING = "running";
    private static final String KEY_ACCUMULATED = "accumulated";
    private static final String KEY_START = "start";
    private static final String KEY_RECREATE = "recreate";
    private static final String KEY_CB_STATE = "cb_state"; 
    private static final String KEY_LAP_LIST = "lap_list"; // Khóa lưu danh sách Lap

    private TextView tvTime, tvStatus, tvRecreate, tvLapList;
    private Button btnStartPause, btnReset, btnLap;
    private CheckBox cbStopOnBackground;

    private boolean running = false;
    private long accumulated = 0L;
    private long startTime = 0L;
    private int recreateCount = 0;

    // Mảng lưu danh sách các vòng (Lap)
    private ArrayList<String> lapList = new ArrayList<>();

    private final Handler handler = new Handler(Looper.getMainLooper());
    private final Runnable ticker = new Runnable() {
        @Override
        public void run() {
            updateTimeText();
            handler.postDelayed(this, 100);
        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_main);
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets bars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(bars.left, bars.top, bars.right, bars.bottom);
            return insets;
        });

        // Ánh xạ các View
        tvTime = findViewById(R.id.tvTime);
        tvStatus = findViewById(R.id.tvStatus);
        tvRecreate = findViewById(R.id.tvRecreate);
        tvLapList = findViewById(R.id.tvLapList);
        btnStartPause = findViewById(R.id.btnStartPause);
        btnReset = findViewById(R.id.btnReset);
        btnLap = findViewById(R.id.btnLap);
        cbStopOnBackground = findViewById(R.id.cbStopOnBackground);

        // Khôi phục trạng thái
        if (savedInstanceState != null) {
            running = savedInstanceState.getBoolean(KEY_RUNNING);
            accumulated = savedInstanceState.getLong(KEY_ACCUMULATED);
            startTime = savedInstanceState.getLong(KEY_START);
            recreateCount = savedInstanceState.getInt(KEY_RECREATE) + 1;

            boolean isChecked = savedInstanceState.getBoolean(KEY_CB_STATE, false);
            if (cbStopOnBackground != null) {
                cbStopOnBackground.setChecked(isChecked);
            }

            // Khôi phục danh sách Lap
            ArrayList<String> savedLapList = savedInstanceState.getStringArrayList(KEY_LAP_LIST);
            if (savedLapList != null) {
                lapList = savedLapList;
                updateLapUi();
            }

            Log.d(TAG, "onCreate: KHÔI PHỤC trạng thái");
        }

        // Sự kiện Bắt đầu / Tạm dừng
        btnStartPause.setOnClickListener(v -> {
            if (running) {
                pauseStopwatch();
            } else {
                startStopwatch();
            }
        });

        // Sự kiện nút Vòng (Lap)
        btnLap.setOnClickListener(v -> {
            if (running) {
                String currentTime = tvTime.getText().toString();
                lapList.add("Vòng " + (lapList.size() + 1) + ": " + currentTime);
                updateLapUi();
            }
        });

        // Sự kiện Đặt lại (Reset)
        btnReset.setOnClickListener(v -> {
            resetStopwatch();
            tvTime.setTextColor(Color.BLACK); 

            // Xóa trắng danh sách Lap
            lapList.clear();
            updateLapUi();

            // Rung thiết bị
            Vibrator vibrator = (Vibrator) getSystemService(Context.VIBRATOR_SERVICE);
            if (vibrator != null && vibrator.hasVibrator()) {
                if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
                    vibrator.vibrate(VibrationEffect.createOneShot(150, VibrationEffect.DEFAULT_AMPLITUDE));
                } else {
                    vibrator.vibrate(150);
                }
            }
        });

        updateUi();
    }

    // ---------------- Logic đồng hồ ----------------
    private long elapsed() {
        return running ? accumulated + (SystemClock.elapsedRealtime() - startTime) : accumulated;
    }

    private void startStopwatch() {
        running = true;
        startTime = SystemClock.elapsedRealtime();
        startTicking();
        updateUi();
    }

    private void pauseStopwatch() {
        accumulated += SystemClock.elapsedRealtime() - startTime;
        running = false;
        stopTicking();
        updateUi();
    }

    private void resetStopwatch() {
        running = false;
        accumulated = 0L;
        startTime = 0L;
        stopTicking();
        updateUi();
    }

    private void startTicking() {
        handler.removeCallbacks(ticker);
        handler.post(ticker);
    }

    private void stopTicking() {
        handler.removeCallbacks(ticker);
    }

    // ---------------- Cập nhật giao diện ----------------
    private void updateTimeText() {
        long ms = elapsed();
        long phut = ms / 60000;
        long giay = (ms % 60000) / 1000;
        long phanMuoi = (ms % 1000) / 100;
        tvTime.setText(String.format(Locale.getDefault(), "%02d:%02d.%d", phut, giay, phanMuoi));

        if (ms > 60000) { 
            tvTime.setTextColor(Color.RED);
        } else {
            tvTime.setTextColor(Color.BLACK); 
        }
    }

    private void updateUi() {
        updateTimeText();
        btnStartPause.setText(running ? R.string.pause : R.string.start);
        tvStatus.setText(running ? R.string.status_running : R.string.status_paused);
        tvRecreate.setText(getString(R.string.recreate_count, recreateCount));
    }

    // Cập nhật TextView hiển thị danh sách Lap
    private void updateLapUi() {
        StringBuilder sb = new StringBuilder();
        for (String lap : lapList) {
            sb.append(lap).append("\n");
        }
        tvLapList.setText(sb.toString());
    }

    // ---------------- Vòng đời ----------------
    @Override
    protected void onStart() {
        super.onStart();
    }

    @Override
    protected void onResume() {
        super.onResume();
        if (running) {
            startTicking();
        }
        updateUi();
    }

    @Override
    protected void onPause() {
        super.onPause();
        stopTicking();
    }

    @Override
    protected void onStop() {
        super.onStop();
        if (cbStopOnBackground != null && cbStopOnBackground.isChecked() && running) {
            pauseStopwatch();
        }
    }

    @Override
    protected void onRestart() {
        super.onRestart();
    }

    @Override
    protected void onDestroy() {
        stopTicking();
        super.onDestroy();
    }

    // ---------------- Lưu & khôi phục trạng thái ----------------
    @Override
    protected void onSaveInstanceState(Bundle outState) {
        super.onSaveInstanceState(outState);
        outState.putBoolean(KEY_RUNNING, running);
        outState.putLong(KEY_ACCUMULATED, accumulated);
        outState.putLong(KEY_START, startTime);
        outState.putInt(KEY_RECREATE, recreateCount);

        if (cbStopOnBackground != null) {
            outState.putBoolean(KEY_CB_STATE, cbStopOnBackground.isChecked());
        }

        // Lưu danh sách Lap vào Bundle
        outState.putStringArrayList(KEY_LAP_LIST, lapList);
    }

    @Override
    protected void onRestoreInstanceState(Bundle savedInstanceState) {
        super.onRestoreInstanceState(savedInstanceState);
    }
}
