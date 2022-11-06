# Resources

## **namelist.input**
```
cat <<EOF > namelist.input
 &time_control
 run_days                            = 0,
 run_hours                           = 18,
 run_minutes                         = 0,
 run_seconds                         = 0, 
 start_year                          = 2021,
 start_month                         = 06,
 start_day                           = 29,
 start_hour                          = 00,
 start_minute                        = 00,
 start_second                        = 00,
 end_year                            = 2021,
 end_month                           = 06,
 end_day                             = 29,
 end_hour                            = 18,
 end_minute                          = 00,
 end_second                          = 00,
 interval_seconds                    = 21600
 input_from_file                     = .true.,
 history_interval                    = 60,
 frames_per_outfile                  = 1,
 restart                             = .false.,
 restart_interval                    = 10000,
 io_form_history                     = 2,
 io_form_restart                     = 2,
 io_form_input                       = 2,
 io_form_boundary                    = 2,
 /

 &domains
 perturb_input                       = .false.
 time_step                           = 10,
 time_step_fract_num                 = 0,
 time_step_fract_den                 = 1,
 max_dom                             = 1,
 s_we                                = 1,
 e_we                                = 100, 
 e_sn                                = 127,
 e_vert                              = 45,
 dx                                  = 15000,
 dy                                  = 15000,
 grid_id                             = 1, 
 parent_id                           = 1,
 i_parent_start                      = 1,
 j_parent_start                      = 1,
 parent_grid_ratio                   = 1,
 parent_time_step_ratio              = 1,
 feedback                            = 1,
 smooth_option                       = 0
 num_metgrid_levels                  = 34,
 num_metgrid_soil_levels             = 4,
 /

 &physics
 physics_suite                       = 'tropical'
 mp_physics                          = 6,
 ra_lw_physics                       = 4,
 ra_sw_physics                       = 4,
 radt                                = 30,
 sf_sfclay_physics                   = 91,
 sf_surface_physics                  = 2,
 bl_pbl_physics                      = 1,
 bldt                                = 0,
 cu_physics                          = 16,
 cudt                                = 0,
 isfflx                              = 1,
 ifsnow                              = 0,
 icloud                              = 1,
 surface_input_source                = 1,
 num_soil_layers                     = 1,
 maxiens                             = 1,
 maxens                              = 1,
 maxens2                             = 1,
 maxens3                             = 1,
 ensdim                              = 1,
 /

 &dynamics
 w_damping                           = 0,
 diff_opt                            = 2,
 km_opt                              = 4,
 khdif                               = 0,
 kvdif                               = 0,
 non_hydrostatic                     = .true.,
 moist_adv_opt                       = 1,
 scalar_adv_opt                      = 1,
 use_baseparam_fr_nml = .t.
 /

 &bdy_control
 spec_bdy_width                      = 5,
 spec_zone                           = 1,
 relax_zone                          = 4,
 specified                           = .true., 
 nested                              = .false.,
 /

 &namelist_quilt
 nio_tasks_per_group = 0,
 nio_groups = 1,
 /
EOF
```

## **namelist.wps**

```
cat <<EOF > namelist.wps
&share
 wrf_core = 'ARW',
 max_dom = 1,
 start_date = '2021-06-30_00:00:00','2021-06-30_00:00:00',
 end_date   = '2021-06-30_18:00:00','2021-06-30_18:00:00',
 interval_seconds = 21600
/

&geogrid
 parent_id         =   1,   1,
 parent_grid_ratio =   1,   3,
 i_parent_start    =   1,  53,
 j_parent_start    =   1,  25,
 e_we              =  100, 220,
 e_sn              =  127, 214,
 geog_data_res = 'default','default',
 dx = 4100,
 dy = 4100,
 map_proj = 'mercator',
 ref_lat   =  5.464,
 ref_lon   =  100.289,
 truelat1  =  5.464,
 truelat2  =  0,
 stand_lon =  100.261,
 geog_data_path = '/shared/scratch/WRF_Resources/WPS_GEOG/'
/

&ungrib
 out_format = 'WPS',
 prefix = 'FILE',
/

&metgrid
 fg_name = 'FILE'
/
EOF
```