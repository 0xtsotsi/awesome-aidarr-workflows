



# trace-to-svg

Convert a bitmap into a vector SVG using `mkbitmap` + `potrace`.

## Quick start

```bash
# 1) Produce a silhouette-friendly SVG
bash scripts/trace_to_svg.sh input.png --out out.svg

# 2) Higher contrast + less noise
bash scripts/trace_to_svg.sh input.png --out out.svg --threshold 0.6 --turdsize 20

# 3) Feed into create-dxf (example)
# - set create-dxf drawing.etch_svg_paths[].d to the SVG path `d` you want, or
# - store the traced SVG and reference it in your pipeline.
```

## Notes

- This is best for **logos, silhouettes, high-contrast shapes**.
- For photos or complex shading, results depend heavily on thresholding.
- Output is usually one or more `<path>` elements.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
