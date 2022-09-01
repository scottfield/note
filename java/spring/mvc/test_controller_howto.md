###Sample code how to test controller in spring MVC
```
package com.synnex.hyve.global.planning.attribute.web;

import com.synnex.hyve.global.planning.attribute.entity.hyvemrp.MaterialBuffer;
import com.synnex.hyve.global.planning.attribute.service.CommonService;
import com.synnex.hyve.global.planning.attribute.service.MaterialBufferService;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;

import java.util.ArrayList;
import java.util.List;

import static org.hamcrest.Matchers.equalTo;
import static org.hamcrest.Matchers.hasSize;
import static org.hamcrest.Matchers.is;
import static org.mockito.Matchers.refEq;
import static org.mockito.Mockito.when;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.jsonPath;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@RunWith(SpringRunner.class)
@WebMvcTest(value = {MaterialBufferController.class})
public class ControllerTest {
    @Autowired
    private MockMvc mockMvc;
    @MockBean
    private MaterialBufferService materialBufferService;
    @MockBean
    private CommonService commonService;

    @Test
    public void testApiAltGroupListGet() throws Exception {
        List<MaterialBuffer> materialBuffers = new ArrayList<>();
        MaterialBuffer buffer = new MaterialBuffer();
        buffer.setCustNo(554401);
        materialBuffers.add(buffer);
        when(materialBufferService.findAll(refEq(new MaterialBuffer()))).thenReturn(materialBuffers);

        mockMvc.perform(get("/api/material-buffers"))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.status", is(200)))
                .andExpect(jsonPath("$.data", hasSize(1)))
                .andExpect(jsonPath("$.data[0].custNo", equalTo(554401)));
    }
}
```
