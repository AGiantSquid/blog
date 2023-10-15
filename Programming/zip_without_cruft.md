```
zip \
  -r [destination].zip [source]/ \
  -x \
    "*/.venv/*" \
    "*/__pycache__/*" \
    "*/.ruff_cache/*"
    "*/.tox/*" \
    "*/dist/*" \
    "*/build/*" \
    "*/node_modules/*" \
    "*/.serverless/*" \
    "*/.dynamodb/*" \
    "*/.benchmarks/*" \
    "*/.terraform/*" \
    "*/.git/*" \
    "*/_build/*" \
    "*/artifacts/*" \
```    
