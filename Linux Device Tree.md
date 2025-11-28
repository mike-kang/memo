## machine
예전 방식
```
MACHINE_START(MYBOARD, "MyBoard")
    .map_io = ...,
    .init_irq = ...,
    .init_machine = myboard_init,
MACHINE_END
```
DT 방식
```
DT_MACHINE_START(ROCKCHIP_DT, "Rockchip (Device Tree)")
    .l2c_aux_val    = 0,
    .l2c_aux_mask   = ~0,
    .init_time      = rockchip_timer_init,
    .dt_compat      = rockchip_board_dt_compat,
    .init_machine   = rockchip_dt_init,
MACHINE_END
```

## i2c
예전 방식
```
static struct bma150_platform_data bma150_pdata = {
    .cfg = { ... },
};

static struct i2c_board_info bma150_info[] = {
    {
        I2C_BOARD_INFO("bma150", 0x38),
        .platform_data = &bma150_pdata,
        .irq = GPIO_TO_IRQ(...),
    },
};

static void __init my_board_i2c_init(void)
{
    i2c_register_board_info(1, bma150_info,
                            ARRAY_SIZE(bma150_info));
}
```
DT 방식
```
&i2c1 {
    bma150@38 {
        compatible = "bosch,bma150";
        reg = <0x38>;
        interrupt-parent = <&gpio0>;
        interrupts = <5 IRQ_TYPE_EDGE_FALLING>;
    };
};
```

# symbol 의미
## #address-cells #size-cells

여기서 celldms 32bit를 의미
자신의 child device address 의 크기와 child device 가 차지하는 memory

ex)
```
i2c1: i2c@ff140000 {
	reg = <0x0 0xff140000 0x0 0x1000>;
	#address-cells = <1>;
	#size-cells = <0>;
};
```
"i2c1에 child device의 address가 32bit 주소에 메모리는 차지하지 않는다."란 의미이다.