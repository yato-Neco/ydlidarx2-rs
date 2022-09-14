# ydlidarx2-rs


This crate is for using YDLIDAR X2 in Rust.


### Cargo.toml
```
[dependencies]

ydlidarx2-rs = { git = "https://github.com/yato-Neco/ydlidarx2-rs.git", branch = "master"}

```

### Example

```
let mut port = match serialport::new("COM4", 115200)
        .stop_bits(serialport::StopBits::One)
        .data_bits(serialport::DataBits::Eight)
        .timeout(Duration::from_millis(10))
        .open()
    {
        Ok(p) => (p),
        Err(_) => (panic!()),
    };

    let mut serial_buf: Vec<u8> = vec![0; 500];

    loop {
        match port.read(serial_buf.as_mut_slice()) {
            Ok(t) => {
                let mut data = serial_buf[..t].to_vec();

                let points =  ydlidarx2_rs::ydlidarx2(&mut data);
              
                }
            }

            Err(_) => {}
        }
    }

```